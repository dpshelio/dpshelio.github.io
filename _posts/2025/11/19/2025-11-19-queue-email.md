---
layout: post
title: "Queuing email on emacs using mu and msmtp"
date: 2025-11-19
time: "16:45:00"
blog: "true"
categories: ["email", "emacs", "learning"]
---

*TL;DR: [jump to the end](#all-together) to see all together if you don't care about my learning process*

I've started to use [`mu4e`][mu4e] a while ago, motivated by the
instructions shared on [M-x Research][m-x-research] when Martin
Richter showed us how to do it.

One thing I'd like to have is a send-later feature as outlook and
gmail allows you to do so. So I can schedule an email to be sent on a
particular day. Unfortunately I've not found a way to do so yet that
works for me. I've been told that [gnus][gnus] has an option to do so, but
you'll need a computer switched on waiting that the time comes. I have
some ideas on how that could be implemented for Outlook, but I've not
come around that yet.

An alternative that I'd be happy with is to be able to queue my
email. Either because I don't want to send emails later in the
evening, or just because I'm in a place without internet.
[`mu4e` has the machinery to queue emails][mu4e-queue] as it's shown
in their documentation.
However, it took a while for me to realise what I was missing.
So, hopefully my lines below helps to others and also people can
comment on my elisp so I can improve.

`mu4e` documentation seems straight forward, you need only two
variables being set (`smtpmail-queue-mail` and `smtpmail-queue-dir`)
and that the queue directory actually exists. For much I tried, this
was not working, the emails were either sent, or erroing when I was
disconnected from the net. Reading through the code I figured out that
the issue was that I hadn't configured my email using `smtpmail` emacs
library, but instead [`msmtp`][msmtp] program. I believe the reason is
because the oauth authentication workflow I need for my university
requires that I use [oauth2ms][o2ms] (please, feel free to correct me
if I'm wrong!).

Once I new the cause was there I started thinking on how I could queue
it. This brought me to search those two terms: `msmtp` and
`queue`. And that pointed me to this particular bit of the [source
code of `msmtp`][msmtpqueue]. Some scripts untouched from 17 years ago
(if it works, why touch it, right?). I started to dive into them,
thinking how I could use them, then I realised that on the nav bar on
the left said `emacs`, and I got exited thinking that the solution may
have been there already... but no, it was not. However, that
distraction helped me to find [`msmtpq`][msmtpq]... which I clicked on
it thinking it was what I was trying to digest before. But it was not!

`msmtpq` provides a layer on top of `msmtp` that before sending any
email checks whether you've got a live connection. This seemed
promising!

So, what did I do? I started messing up with my emacs config code, and
look into what mu4e was doing. This is what I come up with.

First, I needed to put the `msmtpq` script on my path. In my Arch distro I had to do:
```bash
cd ~/.local/bin
ln -s /usr/share/doc/msmtp/msmtpq/msmtpq .
ln -s /usr/share/doc/msmtp/msmtpq/msmtp-queue .
```

Then in emacs I had a variable that defines what the `sendmail` program is

```elisp
(setq sendmail-program  (executable-find "msmtp"))
```
and I wanted to change it to the `msmtpq` when I want to queue the email. So I crated a function that depending whether I'm in queue or direct mode (i.e., whether `smtpmail-queue-mail` is true or not) tells what executable to use:

```elisp
(defun dps/queue-or-not ()
  (if smtpmail-queue-mail
      ;; need to set some system variables
      ;; EMAIL_CONN_TEST='q'
      ;; EMAIL_QUEUE_QUIET=1 ;; to keep it quiet
      (progn (setenv "EMAIL_QUEUE_QUIET" "1")
	     (setenv "EMAIL_CONN_TEST" "q")
	     (executable-find "msmtpq")
	     )
    (executable-find "msmtp")
    ))
```

Originally, I had set that `EMAIL_CON_TEST` system variable to `'x'`,
wrongly thinking that it meant that it was not going to be sent, but
it actually means to don't check for internet connection. Since I
wanted to force it to queue even if I had internet, I introduced a new
parameter into `msmtpq`.

```diff
316,317d315
<   elif [ "$EMAIL_CONN_TEST" = 'q' ] ; then                     # force it to queue
<     return 1
```

I've opened a [PR to msmtp to include that option][msmptp#211], in
case this becomes useful for more people.

> *Note to my future self:*  
> In a future refactoring, probably all I need on the function above is
> to set that variable from `'x'` to `'q'`, and always use `msmtpq`.

Once I had that function, I could define the `sendmail-program` to
read from it. So, I tried something like: 

```elisp
(setq sendmail-program  'dps/queue-or-not)
```

And other variants of the above (you know with `#`, with `,`, with all
of them....), but that was not working because where that variable was
used was expecting the path, not a function to execute. So I had to
approach the problem in a different way.

My first approach was to set that variable when I toggle the sending
mode on mu4e, and mu4e has that encapsulated into the
[`mu4e--main-toggle-mail-sending-mode` function][mu4e-toggle-mail].
So, I can copy it and modified, and that's what I did:

```elisp
(defun mu4e--main-toggle-mail-sending-mode ()
  "Toggle sending mail mode, either queued or direct."
  (interactive)
  (unless (file-directory-p smtpmail-queue-dir)
    (mu4e-error "`smtpmail-queue-dir' does not exist"))
  (setq smtpmail-queue-mail (not smtpmail-queue-mail))
  (mu4e-message
   (concat "Outgoing mail will now be "
           (if smtpmail-queue-mail "queued" "sent directly")))
  (unless (or (eq mu4e-split-view 'single-window)
              (not (buffer-live-p (get-buffer mu4e-main-buffer-name))))
    (setq sendmail-program (dps/queue-or-not))
    (mu4e--main-redraw)))
```

Inserting that `setq` line in the second last line.

Perfect, that works! I can toggle the email on the dashboard, and it
queues or send the email as I need.

Next I wanted to display how many emails were on the queue... and for that I had to rewrite another function, this time [`mu4e--main-queue-size` function][mu4e-queue-size]. And this is how that looks now:

```elisp
(defun mu4e--main-queue-size ()
  (length (directory-files "~/.msmtp.queue" nil "msmtp"))
  )
```

Which essentially counts how many `.msmtp` files are in the queue directory.

And finally, I needed to update flushing the queue command. `mu4e` uses [`smtpmail-send-queued-mail`][smtpmail-send-queued], but I'm not using that anywhere, so I could rewrite as:

```elisp
(defun smtpmail-send-queued-mail ()
  (interactive)
  (setenv "EMAIL_CONN_TEST" "x")
  (shell-command (concat (executable-find "msmtp-queue") " -r &") "*msmstp-queue*")
  )
```

And that's all I needed. I'm not too happy on copy-paste and changing functions, but it works for now. Making me very happy to see that when I change the email mode the interface reflects that and emails get queued or flushed as I want.

...

Till I went to demonstrate it live yesterday on the [Emacs London meetup][emacs-ldn]. There I told them why I did and how so I could get some feedback. And I did.

First, why it was not working when I show it to them? It took me a while to figure it out, and `toggle-debug-on-error` was not helpful. However, I found out that the emails were not being queued because emacs couldn't find `msmtpq`. This happened because I'm starting emacs as a service, and the `$PATH` in that environment doesn't includes `~/.local/bin`. Though surprisingly, if I do `M-! echo $PATH` it does. So I solved it by creating a copy of `emacs.service` into my `~/.config/systemd/user/` where I added:
```
Environment="PATH=~/.local/bin:/usr/local/bin:/usr/bin"
```
and now it works.

Additionally, I've got some "advice" on how to modify the large function I had to copy from mu4e to define the program (and variables) depending of the mode.

So, this 
```elisp
(defun mu4e--main-toggle-mail-sending-mode ()
  "Toggle sending mail mode, either queued or direct."
  (interactive)
  (unless (file-directory-p smtpmail-queue-dir)
    (mu4e-error "`smtpmail-queue-dir' does not exist"))
  (setq smtpmail-queue-mail (not smtpmail-queue-mail))
  (mu4e-message
   (concat "Outgoing mail will now be "
           (if smtpmail-queue-mail "queued" "sent directly")))
  (unless (or (eq mu4e-split-view 'single-window)
              (not (buffer-live-p (get-buffer mu4e-main-buffer-name))))
    (setq sendmail-program (dps/queue-or-not))
    (mu4e--main-redraw)))
```

become

```elisp
(defun dps/mu4e-toggle-mail (orig-func &rest args)
  (setq sendmail-program (dps/queue-or-not))
  (apply orig-func args)
)

(advice-add #'mu4e--main-toggle-mail-sending-mode :around
	    #'dps/mu4e-toggle-mail)
```

Which is a lot nicer and I don't need to keep an eye on what's maintained.


#### All together 

At the end I followed my suggestion above and have just refactor it a
bit more, so this is what I've got.

I need that `smtpmail-queue-dir` variable exists pointing to a `mu`
directory created [as de queuing docs suggest][mu4e-queue], even
though, the emails are not stored there. And I'm going to keep it that
for a bit till I have more time to play.

I'm starting on queueing mode by default and this is how all fits
together (don't forget to modify `msmtpq` to include the `q` as I said
above first):

```elisp
(require 'smtpmail)

(setenv "EMAIL_QUEUE_QUIET" "1")  ;; to keep msmtpq quiet
(setenv "EMAIL_CONN_TEST" "q") ;; queing by default
(setq smtpmail-queue-mail t  ;; start in queuing mode
      smtpmail-queue-dir   "~/Mail/queue/cur" ;; though we are not using it mu4e needs it to be able to toggle
      sendmail-program (executable-find "msmtpq")
      send-mail-function 'message-send-mail-with-sendmail
)

(defun dps/queue-or-not ()
  (if smtpmail-queue-mail
      (setenv "EMAIL_CONN_TEST" "q") ;; queue
      (setenv "EMAIL_CONN_TEST" "x") ;; try to send (will queue if fails)
  )
)

(defun dps/mu4e-toggle-mail (orig-func &rest args)
  (apply orig-func args) 
  (dps/queue-or-not) ;; evaluated after the toggle so we know the smtpmail-queue-mail value
)

(advice-add #'mu4e--main-toggle-mail-sending-mode :around
	    #'dps/mu4e-toggle-mail)

;; rewrite of mu4e--main-queue-size
(defun mu4e--main-queue-size ()
  (length (directory-files "~/.msmtp.queue" nil "msmtp"))
)

;; rewrite of smtpmail-send-queued-mail
(defun smtpmail-send-queued-mail ()
  (interactive)
  (let ((sys_email_conn (getenv "EMAIL_CONN_TEST"))) ;; temp variable to restore the value of varialbe
	   (setenv "EMAIL_CONN_TEST" "x")
       (shell-command (concat (executable-find "msmtp-queue") " -r &") "*msmstp-queue*")
	   (setenv "EMAIL_CONN_TEST" sys_email_conn)
  )
)
```

Any improvements you can think of is highly appreciated! Tell me on
[mastodon][mastodon-comment] or through an [issue on
GitHub][gh-comment].

Thanks to the [Emacs London meetup][emacs-ldn], in particular to Przemek and Eric.


[mu4e]: https://djcbsoftware.nl/code/mu/mu4e/index.html
[mu4e-queue]: https://www.djcbsoftware.nl/code/mu/mu4e/Queuing-mail.HTML
[mu4e-toggle-mail]: https://github.com/djcb/mu/blob/20b2fec339e91051c1aaf303117957c047054540/mu4e/mu4e-main.el#L408-L419
[mu4e-queue-size]: https://github.com/djcb/mu/blob/20b2fec339e91051c1aaf303117957c047054540/mu4e/mu4e-main.el#L379-L386
[smtpmail-send-queued]: https://github.com/emacs-mirror/emacs/blob/master/lisp/mail/smtpmail.el#L421-L478
[m-x-research]: https://m-x-research.github.io/ 
[gnus]: https://gnus.org/
[msmtp]: https://marlam.de/msmtp/
[msmtpqueue]: https://github.com/marlam/msmtp/tree/master/scripts/msmtpqueue
[msmtpq]: https://github.com/marlam/msmtp/tree/master/scripts/msmtpq
[o2ms]: https://github.com/harishkrupo/oauth2ms
[emacs-ldn]: https://emacs.london/
[msmptp#211]: https://github.com/marlam/msmtp/pull/211
[gh-comment]: https://github.com/dpshelio/dpshelio.github.io/issues/new
[mastodon-comment]: https://mastodon.green/@dvdgc13/115578263537884476
