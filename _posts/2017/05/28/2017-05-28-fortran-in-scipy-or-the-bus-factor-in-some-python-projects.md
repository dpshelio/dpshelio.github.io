---
layout: post
title: Fortran in scipy (or the bus factor in some python projects)
date: 2017-05-28
time:"14:57:00"
blog: "true"
categories: [""]
---

A couple of weeks ago I was at [Python in astronomy ][pyastro] conference.
#pyastro is a great place to meet key people behind of a lot of astro-related
projects and to learn and share knowledge with a lot of pycurious astronomers -
I recommend you to read [Sophie's wonderful summary of the conference][sophie].

The morning before we started the hackday someone mentioned `Fortran` and how 
much is used in SciPy (25.6%) as shown in its [GitHub page][scipy].

<img height="98px" alt="scipy stats" src="/gallery/images/2017/05/28/2017-05-28-scipystats.png">

That made me think... How many people do actually know what's going on in these
files? I clicked there, so it took me to [the list of files][scipy_fortran] and
opened a few random files listed there. Surprise! many of these have **only
one** contributor. That made me think even more... *can I get some metrics about 
these files?*. Next morning we had to pitch our ideas for the hack day and, 
of course, I pitched this.

Only [Zé][ze] joined me and between both of us worked our way around git in
python. So we created our [Buss][buss] tool. The tool, is quite simple, it
downloads the repo you want to analyse and give you some simple stats about the
repository such as the number of files that has only one contributor and the
when was the last contribution made for said people.

This simplistic approach shows only the best scenario of the reality. For
example, there may be files with two or more contributors where there's only one
person who actually understand what's in that file and the others contribution
may have been to change the code formatting within the file.

Therefore, if what git tells is the truth (and our program is correct - we need
tests!), then you should take care of some of the people shown as only
contributors of many files. Get them a beer in exchange to explain you what's
going on in these files.

I also need to say that many of these files may be simple files that could
be so simple and correct that no one has had the need to change these. Maybe
new versions of [Buss][buss] include some better ways of measuring that. In
any case I've tried my best to remove known files like `__init__.py` and
similar.

## Let's go with the results!

For the conference I produced some figures for four projects, SciPy (it was who
started it all!), [NumPy][numpy], [Astropy][astropy] and my beloved [SunPy][sunpy].
Now for here I'm expanding this out to all [NumFOCUS][numfocus] python projects.

### How many files has only been touched by one person.

Starting with the four main projects, we found the following:

<!-- cp {sci,num,astro,sun}py/*_total.png . -->
<!-- montage *_total.png -tile x1 -shadow -geometry +1+1 -background none totals.png -->
<img height="98px" alt="files 1 contributor" src="/gallery/images/2017/05/28/2017-05-28-projects_pyastro.png">

And for the other NumFOCUS python projects:

<!-- montage *_total.png -tile 4x2 -shadow -geometry +1+1 -background none totals.png -->
<img height="98px" alt="files 1 contributor" src="/gallery/images/2017/05/28/2017-05-28-projects_numfocus.png">

### Are they active?

For each of these projects we've visualised each author and how many files 
they are the only contributor, coding in colour the years that passed without 
they committing to the repository. Ideally we could obtain the information from
GitHub to get whether they've been active discussing issues and reviewing pull
requests.

<!-- cp {sci,num,astro,sun}py/*_authors.png . -->
<!-- montage *_authors.png -tile x1 -shadow -geometry +1+1 -background none authors.png -->
<img height="98px" alt="endangered authors" src="/gallery/images/2017/05/28/2017-05-28-authors_pyastro.png">
<!-- montage *_authors.png -tile 4x2 -shadow -geometry +1+1 -background none authors.png -->
<img height="98px" alt="endangered authors" src="/gallery/images/2017/05/28/2017-05-28-authors_numfocus.png">


## Next steps

I would say the first obvious step without adding much complexity it could be to
analyse the content of these *critic* files by language, purpose (are they
tests?), etc. If we want to go into more detail we could look the activity of
these contributors to the project (are they still active?), the files with 
other contributors where only formatting changes have be applied (I would have
no idea how to test for that), and finally have a better way to select which
files to count or not (by now I'm only excluding `__init__.py` and `setup_package.py`).
Also, `buss` is only looking to the code directory, not the docs, data, scripts
or other external directories.


[buss]: https://github.com/dpshelio/busfactor
[pyastro]: http://openastronomy.org/pyastro/2017/
[sophie]: http://flarecast.eu/python-in-astronomy
[ze]: https://mirca.github.io/
[numfocus]: 
[astropy]: https://github.com/astropy/astropy
[numpy]: https://github.com/numpy/numpy
[scipy]: https://github.com/scipy/scipy
[scipy_fortran]: https://github.com/scipy/scipy/search?l=fortran
[sunpy]: https://github.com/sunpy/sunpy
