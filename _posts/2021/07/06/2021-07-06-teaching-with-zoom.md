---
layout: post
title: "What the learners see when I use zoom to teach"
date: 2021-07-06
time: "15:24:00"
blog: "true"
categories: ["teaching", "carpentries", "tools", "SwC", "workshops"]
---

Since I started teaching online I thought that a good approach to screen sharing
was to only share half of my desktop. My reasoning being that this way I could
keep the other half of my screen for my teaching notes and the chats (with the
learners and other instructors), whereas the learners could use their other
half for following along.

However, zoom is, by default, configured to switch to full-screen mode when
someone is sharing the screen. It's useful if you are watching some talk or
lecture, but not that much if you need to code-along. As an instructor I didn't
realise this was a problem till a couple of weeks into one of the courses when
a student gave us the following feedback:

> the aspect ratio for Davids screen when he is screensharing means that anything he types is pretty much unreadable.

I believe this is related to that. Also, if the screen gets maximised and I'm
sharing only half of the screen, they get half of the screen in the centre of
their screen, leaving only one quarter on either side to work.

To get ready for my last workshop, and [after multiple problems I've had wit
zoom lately][teaching-obs], I thought it would be better to test how my screen
was seeing on different operative systems and using different clients (the
desktop vs the browser client). Let's see what I found.

In the sections below I'm testing by sharing some files and a terminal running on
VS Code. The sharing was done by [selecting only a portion of the screen option
in the screen sharing menu in zoom][zoom-docs-sharing].

## What would you see when having a single screen?



### Browser vs Zoom desktop app.

First I tried on Linux. On the left, we've got the web client on Firefox, on the
right, the zoom app.

<!-- ![Left shows the zoom interface from Firefox, on the right the zoom interface from the desktop app](/gallery/images/2021/07/2021-07-06-zoom-app-firefox-webcam.png) -->
<img height="400px" alt="Left shows the zoom interface from Firefox, on the right the zoom interface from the desktop app" src="/gallery/images/2021/07/2021-07-06-zoom-app-firefox-webcam.png">

There are already some interesting differences.

1. The area! In the screenshot, the shared area shown by Firefox covers a
   948x1133 px, whereas the desktop zoom app shows 879x1041. In Firefox you get
   17% more than on the desktop.
   
   <!-- ![comparing the shared area of both clients](/gallery/images/2021/07/2021-07-06-zoom-app-firefox-webcam-area.png) -->
   <img height="200px" alt="comparing the shared area of both clients" src="/gallery/images/2021/07/2021-07-06-zoom-app-firefox-webcam-area.png">

   Why is that? Well, because the video from the presenter is shown as a
   floating window, that you can move around (even outside of the view) as you
   please, whereas in Zoom you are stuck to either have it on the top or on the
   side. Ideally, I could control where to appear, but [I've had other problems
   with that][teaching-obs].
   
2. The zoom actions menu. It hides on both applications, however, in Firefox
   doesn't hide any content, whereas it does so in the desktop app.
   
   <!-- ![highlighting the menu bar of both Firefox and Zoom](/gallery/images/2021/07/2021-07-06-zoom-app-firefox-menu-bar.png) -->
   <img height="300px" alt="highlighting the menu bar of both Firefox and Zoom" src="/gallery/images/2021/07/2021-07-06-zoom-app-firefox-menu-bar.png">
   
   I find this very frustrating when you want to see something and the app keeps
   showing you a bar just because you hovered the mouse over. And by the time
   you calm down and stop moving the mouse, the thing you wanted to see is
   gone.
   
Focusing only on the shared screen, we should then prefer to use Firefox over
the desktop app. You get more space and nothing hiding any of the important
bits. However, if you need to also use the chat, then this may not be the best
option. (We tend to not use the chat but a shared document instead).
Additionally, you could even get more space hiding some bits from the firefox
bar that you may not need.

How does this look in the Windows world?

In windows, the first browser I tried was Chrome, and to my surprised, it was
different from Firefox on Linux. A popup appeared with the great news when you
connect saying that you've got now a gallery/images view on Chrome! 🤦 That would have
been awesome if it would let you choose which view you'd like. But it doesn't!

<!-- ![Connecting from Windows, desktop application on the left vs Chrome on the right](/gallery/images/2021/07/2021-07-06-zoom-windows-chrome.png) -->
<img height="300px" alt="Connecting from Windows, desktop application on the left vs Chrome on the right" src="/gallery/images/2021/07/2021-07-06-zoom-windows-chrome.png">

With Firefox, however, you can still get the floating window for the webcams, but
the area is not that different! The desktop app being ~5% larger. Though, the bottom
menu bar will still hide part of the shared screen.



### Multiple screens

If you've got more than one screen then you haven't got many problems with
space, right? However, there's a nice feature of zoom that you can enable when
using multiple screens, [enabling dual monitors][zoom-docs-dual]. This separates
the zoom application into two windows, one for the bits being shared, and another
where you can see the webcam of the participants.

<!-- ![Zoom desktop app with the dual-monitor feature enabled, left half showing the shared content and the right half shows the video participants](/gallery/images/images/2021/07/2021-07-06-zoom-app-windows-multiplescreen.png) -->
<img height="300px" alt="Zoom desktop app with the dual-monitor feature enabled, left half showing the shared content and the right half shows the video participants" src="/gallery/images/2021/07/2021-07-06-zoom-app-windows-multiplescreen.png">

This is the best of all the options! You get the zoom menu bar on the
participants' view, not hiding any of the content! Sadly, you need to have two
screens... or do you? There's some trickery we can do to our computers to make
[zoom believe that there are multiple screens][fake-screen-win] and make this
view available. However, this is not something I can ask my learners to set up
before a class or a workshop. If you start zoom with a second screen connected,
then I believe zoom keeps believing that you have that set up for the following
calls. (Though it seems absurd that you find in such a situation, this trick has
helped me many times where I can steal my girlfriend's second monitor to start zoom
and return it to her afterwards).

## Final thoughts

First of all, I need to tell my students to [disable the "enter full screen when
a participant shares screen" option][zoom-no-fullscreen]. This will at least let
them place the window whenever they want.

Secondly, I need to test and re-test every time before teaching. In my [last
post, I explained why I had to use OBS][teaching-obs]. That worked fine for the
teaching I needed to do in that time which didn't require live-coding. However,
when trying to use OBS to share only half of my screen I found a different
problem. Since Zoom believes it's your webcam that gets transmitted, Zoom keeps a
webcam ratio on the screen, instead of what you normally get from a screen share,
defeating the point of sharing half of the screen.

This time I went to "fix" zoom on my machine, and I did it by trying different
versions you can install in Linux. The one that worked on my machine (Archlinux
with Gnome over Wayland) was using [flatpak][flatpak]. Or so I thought. I run
all these tests, took lots of screenshots to share with my learners the optimal
way to connect. During these tests I had noticed that my mouse pointer was not
seen at all, but that was not new, I had to be more specific with my language.
However, when I started teaching, I got one of the attendees saying "the screen
is not changing"... 😱 Panic moment again! Zoom was not streaming my screen to
the participants. Or well, it was, but only when I was hovering the mouse over
the screen share bar that zoom creates. This meant I had to type and move the
mouse every couple of seconds and made the flow of the workshop not as smooth as
I would have liked it. Updating zoom again a couple of days later (from 5.6.1
to 5.7.xxx) seems to have fixed that issue on my latest tests.

If that was not enough, one of the attendees that tried to follow my indications
to use Firefox on the university desktop couldn't get the sound working,
whereas the zoom app worked fine. Maybe I'll design a flowchart before the next
academic year starts so the students could get the most optimal setup with a
less confusing set of instructions.


[teaching-obs]: {% post_url 2021-05-02-teaching-with-obs.md  %}
[zoom-docs-sharing]: https://support.zoom.us/hc/en-us/sections/201740106-Screen-Sharing
[zoom-docs-dual]: https://support.zoom.us/hc/en-us/articles/201362583-Using-Dual-Monitors-with-the-Zoom-Desktop-Client
[fake-screen-win]: https://answers.microsoft.com/en-us/windows/forum/all/how-to-enable-a-fake-second-display-in-windows-10/3c02e2ee-cade-4916-be46-390e59ea2a04
[zoom-no-fullscreen]: https://makeitallwork.com/how-to-prevent-zoom-automatically-going-full-screen/
[flatpak]: https://www.flatpak.org/
