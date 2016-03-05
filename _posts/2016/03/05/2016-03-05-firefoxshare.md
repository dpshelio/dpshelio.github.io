---
layout: post
title:  "Teaching without showing my notes"
date:   2016-03-05
time:   "20:30:00"
blog:   "true"
categories: ["SwC", "tools"]
---

When I give a talk I try to set my computer in presentation mode, so I can get
extra information on the notes for a particular slide, what's next and how I'm
doing in time. I love being able to do that using either LibreOffice or Google
slides.

Similarly I like to do the same when teaching, but with things like tutorials or
examples on software can become a bit difficult. If you have your projector
screen behind you and you are facing the students then your only solution is to
mirror the screen. Otherwise you endanger yourself to get a neck pain or give
your back to the students while talking being just a one way communication. So,
mirroring the screen allows you to look at your audience while looking to your
screen. But if you have your notes also in the screen everyone see them.

In the software carpentry I did in January - where I thought the command line -
I discovered that I could use [Raniere's][raniere] [split window recipe][split]
in two windows simultaneously by just attaching to the same tmux session:

`tmux attach-session`

This way I can get the following, on one side my notes and terminal in the other
just the terminal:

<img height="200px" alt="Sharing terminal" src="/gallery/images/2016/03/2016-03-05-swc-tmux.png">

It's worth mentioning that I normally login as my normal user in my computer
(where I have all my notes, presentations and stuff) and I open a terminal as a
blank user, so my config files don't get on the way while teaching, so I'm the
closer to the student environment. Since I want to open nautilus and possibly
other stuff, I just need to `xhost +` from my user account to allow the plain
teaching user account to display some windows.

That's for the shell, and it works great! but... two weeks ago I had to teach
python, which is done using jupyter notebooks which goes on top of the browser.
So I looked up every single combinations of words I could think of to do the
same thing: share tabs, display same tab, copy tab, etc... of course, you find
thousands of results but none to do exactly what I wanted: have two firefox
windows that shows the same and scrolls at the same time.

I then went to the [#firefox IRC channel][firefoxIRC] and asked there - the best
as I can... and while doing so (rubber ducking on its best) I thought I could
use `hello` from Firefox, so calling myself and share the screen:

1. Open firefox and start a hello call (it's one of the new things firefox got
   recently)
2. Share tabs and mute mic and camera
3. Open a new firefox session as: `firefox -no-remote -p` (no-remote will allow
   2 firefox running at once, -p gives you profile selection)
4. Connect to the call and allow access to camera and mic (otherwise it doesn't
   work, but they had been blocked by the other); you can mute them afterwards.
5. Select full-screen (right botton) and voilà!

That was producing a bit of a delay, but so far seemed as a good option. Still..
I didn't stop there.. an hour latter I managed to get another solution that was
lot more responsive and you didn't have the pixelation that hello was producing
sometimes while broadcasting the window. This was thanks to a hint given by
[Stuart][stuart], use vnc.

So I installed a vnc server and client (`x11vnc` and `tigervnc`) and proceed
with the following steps.

1. Move your browser window to the screen of the projector, and resize the
   window the size of the screen (pressing full screen does not work because
   when you move it back to yours will be resized).
2. Bring it back to your display.
3. Start te vncserver: `x11vnc -id pick` - and click in the window you want to
   share
4.  Open `tigervnc` and connect to your localhost:0, change certain options
    like:
     - Input/view only
     - Screen/ (not) enable full-screen mode over all monitors (that expands the
   full screen over the two screens) or from the command line as: `vncviewer
   -viewonly localhost:0`
5. That opens a new window that's connected with the other one and you can move it to the display.
6. Resize the client window so it doesn't show any of the bars, you can also
   hide the top of it (your browser tabs, apps, ...)

This method was a lot more responsive, however I had to be careful to don't
resize the server window, as doing so killed the vnc connection. In any case, I
prepared myself to that situation in case it happened and I could quickly enough
restart the server and the client in less than a second.

This is how it looks the result, and as you can see I can get my notes and the
browser in one display while the other just pays attention to the notebook.

<img height="200px" alt="Sharing terminal" src="/gallery/images/2016/03/2016-03-05-swc-firefox.png">

Hope this helps to others to provide better experiences for the students and to
the instructors.

[raniere]: https://github.com/rgaiacs
[split]: https://github.com/rgaiacs/swc-shell-split-window
[firefoxIRC]: http://chat.mibbit.com/?server=irc.mozilla.org&channel=#firefox
[stuart]: http://stuartmumford.uk/
