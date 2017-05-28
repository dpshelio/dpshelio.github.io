---
layout: post
title: "Fortran in scipy (or the bus factor in some python projects)"
date: 2017-05-28
time: "14:57:00"
blog: "true"
categories: ["python", "community", "tools"]
---

A couple of weeks ago I was at [Python in astronomy][pyastro].
[#pyastro][pyastro_tw] is a great place to meet key people behind of a lot of astro-related
projects and to learn and share knowledge with a lot of pycurious astronomers -
I recommend you to read [Sophie's wonderful summary of the conference][sophie].

The morning before we started the hackday someone mentioned `Fortran` and how 
much is used in SciPy (25.6%) as shown in its [GitHub page][scipy].

<img width="628px" alt="scipy stats" src="/gallery/images/2017/05/28/2017-05-28-scipystats.png">

That made me think... How many people do actually know what's going on in these
files? I clicked there, so it took me to [the list of files][scipy_fortran] and
opened a few random files. Surprise! many of these have **only
one** contributor. That made me think even more... *can I get some metrics about 
these files?* Next morning we had to pitch our ideas for the hack day and, 
of course, I pitched this.

Only [Zé][ze] joined me and between both of us worked our way around the git API
in python. So we created our [Buss][buss] tool. The tool, is quite simple, after
you download the repo you want to analyse and run it, it gives you some
stats about the repository such as the number and list of files that have only one
contributor and when was the last contribution to the repository made for said people.

In my opinion, this simplistic approach shows only the best scenario of the
cruel reality. For example, there may be files with two or more contributors
where there's only one person who actually understand what's in that file and
the others' contributions may have been changes to the code formatting within the
file.

Therefore, if what git tells is the truth (and our program is correct - we need
tests!), then you should take care of some of the people shown as only
contributors of many files. Why don't you get them a beer in exchange to explain you what's
going on in these files?

I also need to say that many of these files may be so trivial that no one has
had the need to modified or add anything to them. Maybe new versions
of [Buss][buss] include some better ways of measuring that. In any case I've
tried my best to remove known files such as `__init__.py`.

## Let's go with the results!

For the conference I produced some figures for four projects, [SciPy][scipy] (it was who
started it all!), [NumPy][numpy], [Astropy][astropy] and my beloved [SunPy][sunpy].
Now for here I'm expanding this out to all [NumFOCUS][numfocus] python projects and
other python communities I am familiar with so to get a better picture.

### How many files has only been touched by one person.

Starting with the four main projects, we found the following:

<!-- cp {sci,num,astro,sun}py/*_total.png . -->
<!-- montage *_total.png -tile x1 -shadow -geometry +1+1 -background none totals.png -->
<a href="/gallery/images/2017/05/28/2017-05-28-projects_pyastro.png"><img width="625px" alt="files 1 contributor" src="/gallery/images/2017/05/28/2017-05-28-projects_pyastro.png"></a>

For the NumFOCUS python projects ([IPython][ipython], [matplotlib][mpl], [pandas][pandas],
[Pymc3][pymc], [Stan][stan], [PyTables][pytables], [QuantEcon][quantecon] and [yt][yt]):

<!-- montage *_total.png -tile 4x2 -shadow -geometry +1+1 -background none totals.png -->
<a href="/gallery/images/2017/05/28/2017-05-28-projects_numfocus.png"><img width="625px" alt="files 1 contributor" src="/gallery/images/2017/05/28/2017-05-28-projects_numfocus.png"></a>

and the final four ([django][django], [Scikit-image][skimage], [Scikit-learn][sklearn] and
[SQLAlchemy][sqlalchemy]):
<a href="/gallery/images/2017/05/28/2017-05-28-projects_others.png"><img width="625px" alt="files 1 contributor" src="/gallery/images/2017/05/28/2017-05-28-projects_others.png"></a>

### Are they active?

For each of these projects we've visualised each author and how many files 
they are the only contributor, coding in colour the years that passed without 
they committing to the repository. Ideally we should obtain the information from
GitHub to get whether they've been active discussing issues and reviewing pull
requests.

<!-- cp {sci,num,astro,sun}py/*_authors.png . -->
<!-- montage *_authors.png -tile x1 -shadow -geometry +1+1 -background none authors.png -->
<a href="/gallery/images/2017/05/28/2017-05-28-authors_pyastro.png"><img width="625px" alt="endangered authors" src="/gallery/images/2017/05/28/2017-05-28-authors_pyastro.png"></a>
<!-- montage *_authors.png -tile 4x2 -shadow -geometry +1+1 -background none authors.png -->
<a href="/gallery/images/2017/05/28/2017-05-28-authors_numfocus.png"><img width="625px" alt="endangered authors" src="/gallery/images/2017/05/28/2017-05-28-authors_numfocus.png"></a>
<a href="/gallery/images/2017/05/28/2017-05-28-authors_others.png"><img width="625px" alt="endangered authors" src="/gallery/images/2017/05/28/2017-05-28-authors_others.png"></a>

If you know someone named towards the bottom of the plots, and they are in
yellow means that the project need to find quickly some replacement. If the
person at the bottom has a lot of files and it's not so yellowish, then try to
take some time to work on these files.

Here's the list by project:
- [astropy](/gallery/images/2017/05/28/critic/astropy_critic.txt)
- [numpy](/gallery/images/2017/05/28/critic/numpy_critic.txt)
- [scipy](/gallery/images/2017/05/28/critic/scipy_critic.txt)
- [sunpy](/gallery/images/2017/05/28/critic/sunpy_critic.txt)
- [IPython](/gallery/images/2017/05/28/critic/ipython_critic.txt)
- [matplotlib](/gallery/images/2017/05/28/critic/matplotlib_critic.txt)
- [pandas](/gallery/images/2017/05/28/critic/pandas_critic.txt)
- [Pymc3](/gallery/images/2017/05/28/critic/pymc3_critic.txt)
- [Stan](/gallery/images/2017/05/28/critic/pystan_critic.txt)
- [PyTables](/gallery/images/2017/05/28/critic/PyTables_critic.txt)
- [QuantEcon](/gallery/images/2017/05/28/critic/QuantEcon.py_critic.txt)
- [yt](/gallery/images/2017/05/28/critic/yt_critic.txt)
- [django](/gallery/images/2017/05/28/critic/django_critic.txt)
- [Scikit-Image](/gallery/images/2017/05/28/critic/scikit-image_critic.txt)
- [Scikit-Learn](/gallery/images/2017/05/28/critic/scikit-learn_critic.txt)
- [SQLAlchemy](/gallery/images/2017/05/28/critic/sqlalchemy_critic.txt)


## Next steps

I would say the first obvious step without adding much complexity it could be to
analyse the content of these *critic* files by language, purpose (are they
code or tests?), etc. 

If we want to go into more detail we could look at:
 - the activity of these contributors to the project (are they still active?), 
 - the files with other contributors where only formatting changes have be applied (I would have
no idea how to test for that),
 - and finally have a better way to select which files to count or not (by now
I'm only excluding `__init__.py` and `setup_package.py`). 

Also, notice that `buss` is only looking to the code directory, not the docs,
data, scripts or other external directories.


[buss]: https://github.com/dpshelio/busfactor
[pyastro]: http://openastronomy.org/pyastro/2017/
[pyastro_tw]: https://twitter.com/search?q=%23pyastro17
[sophie]: http://flarecast.eu/python-in-astronomy
[ze]: https://mirca.github.io/
[numfocus]: https://www.numfocus.org/open-source-projects/
[astropy]: https://astropy.org
[numpy]: https://github.com/numpy/numpy
[scipy]: https://github.com/scipy/scipy
[scipy_fortran]: https://github.com/scipy/scipy/search?l=fortran
[sunpy]: http://sunpy.org
[ipython]: http://ipython.org/
[mpl]: http://matplotlib.org/
[pandas]: http://pandas.pydata.org
[pymc]: https://github.com/pymc-devs/pymc3
[stan]: http://mc-stan.org/interfaces/pystan
[pytables]: http://www.pytables.org
[quantecon]: https://quantecon.org/python_index.html
[yt]: http://yt-project.org/
[django]: https://www.djangoproject.com/
[sklearn]: http://scikit-learn.org
[skimage]: http://scikit-image.org
[sqlalchemy]: http://sqlalchemy.org
