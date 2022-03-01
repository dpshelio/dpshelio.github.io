---
layout: post
title: "February: a 'functional' month"
date: 2022-03-01
time: "18:45:00"
blog: "true"
categories: ["learning", "emacs"]
---

Long time no see!! I should write more often in here, right?

We've started a new month in this year (yeah 2022 already) and I've been
yesterday and today wishing `x2` happy new year (i.e., for 2021 and 2022) to so
many colleagues I've not seen since we left the offices. So, Happy new years to
you too!!

I've took over the "organisation" of the [M-x Research group][m-x-research] - an
[emacs] group for people working on research projects. We've [planned some
activities for this year][m-x-2022], and one of them was making February a
functional month - i.e., to practice some elisp by our own solving some problems
and share it with the group for feedback and encouragement. Unfortunately, I
don't think I did a good job advertising this challenge as I think I've been the
only one trying to do it, and this February had a lot of strikes in UK
universities, making it harder for people to engage with volunteering activities.

Nevertheless, I managed to do some of it! In average I've done 1 problem every
two days! (and I'll try to continue learning on March). Here I try to summarise
how has been my learning voyage so far.

## Learning elisp

I've been an [emacs] user since early 2000s. I still remember the first time I
saw the emacs window and how confused I was with the word \*buffers\*. I only
learnt things here and there from a printed copy of the emacs manual that was in
the student's computer room at my uni. Over the years I learnt that the
configuration of the editor was managed by some weird language that used a lot
of parenthesis and without knowing much about it and via copy&paste I got to set
up things somehow right for me. It hasn't been till two years ago that I started
to consider learning that magic language. I have tried without really
progressing much learning lisp from 

- [Structure and Interpretation of Computer Programs][sicp], via reading the book and [watching the classes from 1986][sicp-videos]; and 
- [Land of Lisp][LoL] book.

I didn't really stick to any of these... other things happened and I didn't progress much.

This year, however, it's been a bit different! Our first event of [M-x
Research][m-x-research] was an introduction to (e)lisp: [Functional programming:
an (Emacs) Lisp view 1/n][lisp-intro] ([slides][lisp-intro-slides]) by Jens
Jensen. That was on the first of February and I had already "decided" that
February was going to be a functional month.

From what I learnt that day I set the goal to solve all the [exercism] problems
on the [elisp track][ex-elisp].

[exercism] is an online platform that contains some programming problems to be
solved directly on the website (similar to [codewars]). Once you submit your
solution it allows you to see how others have solved the same problem.

There are 28 exercises for elisp, and I thought it would be great if I could do
one a day. It turned out I have only manged to complete 14 of them, but I'm so
so so happy of my progress!

One of the things I'm more impressed with - and I don't know whether that's a
good practice on functional languages yet - is that I've not created any
variable on any of the problems and that many of the problems had my head
spinning with recursion. Also, how many things from Jens's talk "clicked" at
different times during these exercises - I probably should re-watch that as
there are probably many other things I hadn't absorbed and I've not realised
yet.

I've [saved my progress on a repository][ex-repo], and included [a file with
things I was learning as I was going][ex-learnt]. During this set of exercises
I've learnt to use the `info` command in emacs (`C-h i`), and how to search in
the [elisp manual]. Interestingly, I've only read so far the firs four sections,
up to lists, and it feels as I have super powers now. I can't even imagine
what I'll be able to do when I read the other 37 other sections!

I've also starting to understand how to read the error messages and it has also
helped me to debug problems that have appeared on emacs modules during this time.

In summary, [Jens's lecture][lisp-intro] helped a lot to get me started,
[exercism] has been a great companion to get me "motivated" and to learn how
others have solved the same problem (I still need to investigate the mentoring
program they offer), and though the problems I've solved are labelled as easy,
it feels so good to achieve these little things day after day. Now lisp doesn't
look that mysterious to me (well, it still does, but I can read it now!).

👋 Thanks for reading!




[m-x-research]: https://m-x-research.github.io/ 
[emacs]: https://www.gnu.org/software/emacs/
[m-x-2022]: https://m-x-research.github.io/2022/01/21/a-new-year.html
[sicp]: https://mitpress.mit.edu/sites/default/files/sicp/index.html
[sicp-videos]: https://www.youtube.com/watch?v=-J_xL4IGhJA&list=PLE18841CABEA24090
[LoL]: http://landoflisp.com/
[lisp-intro]: https://www.youtube.com/watch?v=MMRAfd9_d6k
[lisp-intro-slides]: http://purl.org/net/epubs/work/51348587
[exercism]: https://exercism.org/
[ex-elisp]: https://exercism.org/tracks/emacs-lisp
[codewars]: https://www.codewars.com/
[ex-repo]: https://github.com/dpshelio/exercism-voyage
[ex-learnt]: https://github.com/dpshelio/exercism-voyage/blob/main/elisp/learning-elisp.org
[elisp manual]: https://www.gnu.org/software/emacs/manual/html_node/elisp/
