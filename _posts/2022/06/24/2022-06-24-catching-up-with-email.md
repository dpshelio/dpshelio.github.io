---
layout: post
title: "Catching up with e-mail after a holiday break"
date: 2022-06-24
time: "16:30:00"
blog: "true"
categories: ["email", "work", "holidays"]
---

I'm just back from two weeks of holidays and one week of workshop. Normally I
only set my Out of Office email saying something like.

> I'm off till D Month. I'll be come back to you as soon as I can after that day.

That kind of message doesn't help anyone. I'm giving a false hope that I'll
reach to that email and when I'm back in the office I get overwhelmed with the
large amount of emails I've collected while I was away.

This time, and induced by reading ["A world without email" book by Cal
Newport](http://www.worldcat.org/oclc/1241252289) I had first decided to change
the OoO message to:

> I'm off till D Month. Your email has been deleted, send it again when I've returned.

However, while discussing the plans with a colleague who made me think on the
pressure that this may put on others, I considered a different approach. This
was my OoO for the last three weeks:


> Hi there!
> I'm away enjoying my holidays (till the 20th) or at a workshop (20th-24th)!
> 
> TL;DR: Your email is safe – eventually, I'll come back to you. You need
> something urgently – jump to the end of the email.
> 
> I was planning to delete any incoming email while I was away, and let you know
> about such actions. But a good friend has made me rethink this course of
> action, as doing, so I'd be putting the burden on you! What am I doing
> instead? Glad you've asked!! I'm archiving all the emails received during my
> time off under a special folder. When I'm back, a little program will be
> pulling two random emails a day into my inbox, and I commit to answer these.
> How long it will pass before I answer you will depend on luck and the number
> of emails I may have received. By doing so I'll have a better start and don't
> get overwhelmed by a large amount of things to pay attention to.
> 
> Something urgent about
> [...]
> 
> Have a great time (I'll make sure I'll be doing so)!!
> David
> 
> PS: You can trick this system (and this is allowed!) by sending me a reply to
> the original email when I'm back. This way, the old email will resurface
> again!

I've received various positive comments from people who received this OoO and my
Inbox is empty. So, I suppose this approach has worked well... at least till
now. I checked the number of emails I've got in that separate folder this
morning and it would take me more than 9 months to go through them. Let's see
who are the lucky ones that get replied this month.

What's the "technical side" of this? I first attempted to do something very
fancy with [MS Power Automate](https://emea.flow.microsoft.com/en-us/), which
allows to grab emails from your account and do a set of things. However, I got
stuck with the random selection. Their email tool they have only take 25 emails
and that would only benefit at those who wrote closer to my return. I also tried
to come up with some spreadsheet formulae, but that also failed.

First of all I created a rule on the outlook web client. I've set it so that all
the emails with me in the "To" field were going to be archived in the
`OnHolidays` folder. The rest of emails are redirected to `OnHolidaysSecondary`.
I'll be drawing random emails from the primary folder till is empty, then go to
the Secondary (which it should be less important things - I think!)

At the end, I went for a simple approach with the tools I'm more familiar: emacs
and unix tools. I'm reading my email there, so why not do the random selection
from there too? Using org-mode and the `mu` command I come up with the
following:

```bash
mu find -u maildir:'/OnHolidays' -f "i l" | sort | uniq |  awk '{print rand()*1000000, $1, $2}' | sort | head -n 2 | awk '{print  "mu4e:msgid:"$2}'
```

The result of that looks something like: 
```
mu4e:msgid:VI1PR01MB5135E9E1D4A1C701E11F182FC0A39@VI1PR01MB5135.eurprd01.prod.exchangelabs.com
mu4e:msgid:AM6PR0102MB314123DDE920ACBFA727172BADA39@AM6PR0102MB3141.eurprd01.prod.exchangelabs.com
```

which in emacs are clickable links to that particular email on my mu4e views.

I hope this is helpful
