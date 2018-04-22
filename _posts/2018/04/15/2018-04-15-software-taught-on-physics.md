---
layout: post
title: "Software taught on physics"
date: 2018-04-15
time: "21:45:00"
blog: "true"
categories: ["SwC", "community", "software", "teaching", "astronomy", "tools"]
---

A few months ago I was invited to talk at EWASS/NAM session on Software in Astronomy about
training options available for improving astronomers' software development skills. I accepted
the challenge and delivered a talk in such conference on the 4th of April.

## Observations

In my case I only got three to four hours on FORTRAN 77 as part of the compulsory
training. As optional subjects - and thanks to the astrophysics department in my university -
I got more hours of training on shell scripting, IRAF and IDL.
So I wanted to confirm whether similar things happened in other universities and give
a better overview in the talk. What did I do? I run a survey!

I spent quite a lot trying to create a survey so the entries were easier to analyse. However,
that brought some complexity that I couldn't solve using the free available survey tools.
I started to write my own... but after a few hours I gave up thinking that I was not going
to get many answers anyway. So I generate a simple Google form with couple of questions:

- where did you do your degree (country and university)?
- when did you started your degree?
- What's the name of your degree, master or specialisation?
- and a free text box to list the subjects where you got some software development training,
  the language or tool learnt, and the hours of training.
  
At the moment I thought this was clear enough for everyone. How wrong I was! (or so I believe)

## Pre-processing

I believe some people responded to the "the name of their degree" as the one
they had now and not as the one they coursed (e.g. "PhD" versus "degree on
Physics"). Also, in the hours of training some put the length of the course -
not the hours they were taught. In addition there's the problem that in
different countries they have different understanding of what they mean by
degree. All that is the fault of how designed the questions - i.e. Me!

Anyway, I got 142 responses!! which I need to do a lot of
cleaning. [Open Refine](http://openrefine.org/) helped me a bit to cluster
responses regarding names of degrees and universities, but not that much on the
free text box. That I had to do it manually on an spreadsheet (tool I don't
master!).

I've also not accounted for some software that had only one entry (e.g., lisp) or to 
do with hardware control.

## Analysis

I decided to ignore the degree information as I couldn't trust that. Regarding
the countries distribution I've got only multiple (>20) responses from Ireland,
Spain, UK and USA. From the rest of countries I didn't get much more than a
pair. But I didn't go in detail to compare how they differ.

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_countries.png">

The distribution I've got on when they study was quite broad! I've covered
almost 50 years!

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_years.png">

So I thought to look whether there was a clear distinction between the programming
language that was taught over the years... and this is what I've got (normalised over
the number of people for that year):

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_lang_yearprocedural.png">

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_lang_yearoo.png">

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_lang_yearinterp.png">

Clearly Fortran has been the most common! Python and C++ are getting more people.
Though not all specified which type of Fortran they were taught, 37 entries mentioned
Fortran 77, 21 of them after 1995, with the latest mention on 2012. Only 13 of them were
taught a modern version of Fortran (90 or 95, no newer).

I think it's sad that there's a lot of Fortran 77 being taught in the universities. The
only explanation I could think of about why to do so is so people can work with legacy
code. Problem is that they will keep creating "old" software.

What I was interested to obtain was the amount of training that each person received
and that's what I've got!

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_allhours.png">

where shows how many hours they were taught for which language. I've included
IRAF and Excel (or Origin or similar) here too. 23% of the people said they
didn't got any training at all.

If we remove these two entries the plot becomes like:

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_allhours_programming.png">

And removing the ones who specified that the subject was optional - to get a better 
understanding on what is compulsory:

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_allhours_programming_noopt.png">

Then I decided to remove what people got as "numerical methods" because by the number of
hours listed I believe they put the whole subject not the training on software development:

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_allhours_programming_nonum.png">

And sorting that out:

<img width="620px" alt="answers" src="/gallery/images/2018/04/2018-04-15-swia_allhours_programming_nonum_sorted.png">

That shows us that only 33% got compulsory software development training during their degree.

## Conclusions

I believe that in many physics programmes they think that the programming you
need to learn for your future is about how to solve equations - where probably most of
the cases is to do with data management and data manipulation (such as image processing).
This makes sense looking to the past, how in the 70s and 80s we were using computers as
large calculators. However, now a days, we use them for everything! And the programming
skills that we need have to be updated.

## Solutions

### Change what's taught! (or how)

Degrees are already overloaded! There's no possibility to include new modules. But are
they optimal? I've seen places where during the first year the students have to use some
excel (not trained), then they get some c++ classes for a couple of weeks during second
year. In third year they are told about IDL and in the last year they change to Python.
Each time they need to relearn the basics (data types, flow control, io) but never get
to the practice on how to write good programs. Does this sound familiar to you? Then
lobby in your university to get a more unified programme, that builds on what was 
learnt in previous years.


### Run a Carpentries workshop

[The Carpentries](http://carpentries.org/) (joined Software and Data carpentry)
is a project that provides training mostly to researchers. They are compressed
into a two-day workshop where you learn the basics on a set of tools that will
make your life easier. Their lessons are curated to follow good teaching
practices and maximise learning in that short time. Haven't been on one? Don't
way more! [Try to attend to one](https://software-carpentry.org/workshops/) as a
learner or as a helper and get into this wonderful community. You can also
ask to have one at your institution. My team at UCL delivers between 4 and 7
workshops each year!

Or - even better - ask for the next big conference to host one the weekend
before or the weekend after the conference. That's where you get most of the
students together. AAS meetings
have [done this](https://aas.org/meetings/aas231/events#software-carpentry) for
the last couple of years as part of their career development programme.

In addition to these workshop some of us have [run a couple of a week long workshop
under the Open Astronomy umbrella](http://openastronomy.org/2016/01/15/Workshop.html),
where beyond learning the basic tools that the Carpentries teach, we dive into
other tools like astropy, sunpy yt and others.


### Check what is available by your university

Universities and HPC centres normally offer training too. In UK
[archer](http://www.archer.ac.uk/training/courses/) offers a variety
of courses - check their dependencies flowchart! Similarly happens
in other countries ([ICHEC](https://www.ichec.ie/academic/training-education/training-courses) 
in Ireland).

### Nothing available? Create your own!

In the same manner we do journal clubs in our institutions, you can
plan to do programming clubs. Just send an email to the department and
see who is interested. Share what you know, read other people codes, 
talk about programming. I've been doing it since I was doing my PhD in
the middle of nowhere, and that's what brought me where I am!!

### Contribute to an open source project

All right, you are working alone in a remote place and all the above options
are not possible... but you have internet (otherwise you wouldn't be reading
this) - then go ahead and try to contribute to an open source. Check all
the members under Open Astronomy - they have lots of stuff to do, and your
contributions will help many others. You will learn by doing!! reading others
people code and getting suggestions and help on how to make your contributions
better.


### Raw data and code

The raw data from the survey is available in figshare with
DOI:[10.6084/m9.figshare.6169415.v1](https://doi.org/10.6084/m9.figshare.6169415.v1).
The code as there's nothing novel about it I'm sharing it as a
[gist on github](https://gist.github.com/dpshelio/50726b0096084407bb3437a68858b8d9).
