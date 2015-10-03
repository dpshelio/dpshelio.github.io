---
layout: post
title:  "EuroSciPy 2015 - My first EuroSciPy ever!"
date:   2015-08-31
time:   "19:20:00"
blog:   "true"
categories: ["conference", "python"]
---


This EuroSciPy, and probably the previous ones too, was divided into
three parts: the tutorials, the conference and the sprints. The
following is a review of my experience in such amazing conference.

The tutorials consists on two tracks, the beginners and the
advanced. I enjoy the advanced one, but below I've collected the links
for the other tutorials that were advertised on twitter.  The first
morning we get explained what [Bokeh][bokeh] can do and how to extract
information from images using advanced image processing techniques
through [scikit-image][skimage].  Almost all the tutorials (and many
talks during the conference) used [Jupyter
notebooks][jupyter-notebooks] which makes it easier for the atendees
to follow and repeat what is being taught.  [Bokeh's][bokeh-notebook]
contains a large list of ploting examples and explanations of how to
make your owns plot.  I spent the whole lecture dreaming on
[SolarMonitor][solarmonitor] using it... - I don't think it will be
easy, but eh! that's the cool bit of hacking, right?  On the other
hand, the [notebooks from scikit-image][skimage-notebook] were a bit
hidden - on a hidden branch of [skimage tutorials][skimage-tutorials]
Juan's fork - will that be merged?  In this one I was dreaming, again,
on coronal hole detections.

The afternoon of that first day was to learn a bit of machine learning
using [scikit-learn][sklearn] and statistics.  The scikit-learn bit
was done by the [Cambridge Coding academy][cambridgecoding] people,
where by using a table of wines [we were learning][sklearn-practice]
which one were high or low quality.  On the [statistics
tutorial][stats-tutorial] we were analysing brain sizes using
[pandas][pandas] and [statsmodels][statsmodels].

The second day of tutorials was not so varied, but intense. We started
in the morning with a bit of [Cython][cython], learning how to make
our code more as C/C++ in real time.  [Jupyter][jupyter-notebooks] and
Cython talk very well one with the other, and you get very nice
dropdown explanations of the converted code.  [In the
tutorial][cython-tutorial] we learnt how to create arrays and make
operations and compare them with the other python solutions.  Also we
discussed a bit of the fight between [numba][numba] and
[Cython][cython], and how the speaker thought numba will mostly
win... however, numba has a large dependency, [lvm][lvm] which Cython
does not.  The afternoon of that second day we had a mind-blowing
lecture by [Greg Wilson][greg], the creator of [Software
Carpentry][software-carpentry].  I've met Greg before... but not
personally. I am one of the lucky ones who has done the [instructor
training course][swc-training] from him.  Still, even while I had
heard all what he said on Thursday, I was enjoying as if I was
learning it for first time.  He made lots of historical references to
many things related with education which I couldn't write them all
down.  His favourite two books for learning how to teach are: - [How
Learning Works][how-learning] from Ambrose et al., and - [Building a
better Teacher][building-better] from Elizabeth Green He made as also
to work in small groups to get really good and meaningful [multiple
choice questions][multichoice] and review a lot of the [literature
available][swc-reading] on best practice education (or the [TDD][tdd]
for education).  It was an amazing lecture!  A great way to end the
tutorials, planting the seed in us so we go and teach the world.  The
quote from the talk I like the most is: > "We can engineer social
change with these small numbers (5%) ; we've to push in the same
direction!"  And with this the tutorials ended.  We went for the
dinner... and the conference started next morning.


The conference was full of great stuff! and what better to start a
conference with a very controversial keynote? Such work was done by
[Pieter Hintjens][hintjens] - he has even a [wikipedia article about
himself][Whintjens] - and told us about his experience in
[ZeroMQ][0MQ] and different open source software projects. It seems
most of it is available in [his book][0MQOreilly] ([or in the
guide][0MQguide]), but his main discussion point was about how to
handle the community. Some questions where about "how long can a
pull-request wait to be accepted?" or "what's the best way to keep a
mailing list?" or "how to clean the git history?"  or "when do we
produce releases?"- and his answers: 30 seconds - and make your
problems other's problem by converting such person as mantainer; don't
do a mailing list - you are just looking for troubles;
[Stalin][Wstalin] changed history, we don't; releases (or stable
versions) are made when they are asked for it - master have to be
always broken. His best example is how [Wikipedia][wikipedia]
works. All these coments were quite controversial, and people kept
talking about these for the rest of the conference. Personally I agree
with that way of "working" and I think they way he expressed it was to
make it controversial - and he managed to make it so. However, I also
think puting in practice in a project were I've worked for years may
be a bit difficult... with a fear feeling that everything will fall
down. Probably we all need a bit of experience and move out from our
sphere of confidence.


<!--  ###twtitter feed timeline###   include timeline.html  -->

Next was [Ian Ozsvald][ianozsval] who talked about data cleaning for
data mining of a [recruitment agency][elevate]. In his talk Ian showed
a lot of tools and resources, for example to extract information from
PDFs ([textract][textract], [tika][tika], [CERMINE][cermine] for
papers,...), talked about the ["Turkish I problem"][turkishI] and [how
people can die for such problem][diedot]. Also mentioned about tools
of visualisation like [glueviz][glueviz] or [Seaborn][seaborn], tools
for augmenting data ([Alchemy], [DBPedia],...).  As a closing point he
asked for dirty-data horror stories, he wants to fix those! [Check his
slides for more info][ian_slides].

The conference level did not decreased in any moment, it was mantained
up speaker after speaker. We got an introduction of how to [handle big
data with a small computer][JuanTalk] using stuff like [pytoolz] (with
some [recommended][read_pytoolz] [reading][read_wordcount]). The
following speaker - Mikael Mortensen - did the opposite, a python code
to run in big machines that could compete with the classic ones
(Fortran, C, C++). He did it in just 100 lines of python and in just
one day. Check [his slides to see more
details][MikaelTalk]. Incredible! - I'm just going to use it as an
example to many people that believes we should just use Fortran for
everything... We had also talks about [klepto] (unified persistant
storage), [pyMIC] (a python module for Intel Xeon processors), [pyFR]
(more fluid dynamics and HPC), [JyNI] ([Jython] for scientific code),
[bokeh] and [dask] (a task scheduler), a [talk about Gr][gr] with
[matplotlib] and how to make very interactive plots, a python GUI
toolkit based on web ([flexx]), [Spimagine] a tool to visualise
multi-dimensional data using GPUs and how PyQt has been used to build
a modelling tool for complex geochemical process.  All that was just
in the first day!!!

That evening, with all that information in our head some of us
gathered to have a small sprint, not everyone was going to stay till
Sunday. I participated contributed in the scikit-image one trying to
improve some documentation. [Olivia] and I closed the issue
[#1650][skimage-1650] with our [nice pull-request][skimage-1673],
being that our first contribution to [scikit-image][skimage]. Next
morning I found out in my inbox about a new tool ([datajoy]) that I
could use straight away, [to check][datajoy-1659]
[pull-requests][skimage-1659].

The second day of the conference started with a keynote by Randy
Leveque and how to use jupyter notebooks for teaching, he showed some
[examples][jupyter-washington] and talked about plugins to [grade
notebooks][nbgrader] and how he's working with [sagemath
cloud][sagemath] to use it as a tool to check the students excercises
and progress. My mind got full of ideas on how it could be applied on
teaching software carpentry and sunpy around the world... Next speaker
was [Robin Wilson][rwilson] who talked about [recipy], a tool I saw
how was born (at [Collaborative workshop in Oxford][CWblog]) and I had
advertised during the [Python in Astronomy][pyastroblog] meeting. I'm
looking forward to start using it and never try to find how a plot was
made. [ReScience] was the next topic, a journal completely run in
github which aim is to check how replicable other papers are... I want
that for Solar Physics! I'm sure many papers will be difficult to
re-do. This was followed by [Holo Views][holoviews] a tool to
visualise the data, not plotting it - it create plots for quick data
inspection without having to look in detail how to make them. On that
day we also had talks about how to use jupyter notebooks to track
parallel jobs, quantum simulation graph builders (with [kwant]),
reverse engineering animal vision where flies were track (or driven)
by controling what they were seeing with monitors around them, how
python has helped to [create environments for drug
discovery][drugstalk], to [space mission design][plyadestalk], to
[model living tissues][fliestalk] or even to make people rich with
[probablistic programming and sports analytic][probprogramming] (this
last comment was denied by the speaker - but who to believe now a
days?).

The final hour of the conference was completed by a long list of
ligthning talks - for which I was selected volunteer to manage the
slides of each one - where in just two minutes each we were introduced
to lots of stuff - some examples: [astropy], [women hacks for
nonprofits][whnp], [pycharm] educational edition, how to build a very
nice sphinx gallery (like in the [scikit-learn
gallery][sklearn_gallery]), or how [we can help to cite our
software][citation] by adding a `CITATION.txt` file in our
repositories.

And this was all... (and the posters! [nice winner][posterwinner])
that I can remember that happened in this amazing conference. Next two
editions will happen in [Erlangen, Germany][osm_erlangen]... hopefully
I can repit there too!


[bokeh]: http://bokeh.pydata.org/
[skimage]: http://scikit-image.org/
[jupyter-notebooks]: https://jupyter.org/
[bokeh-notebook]: http://nbviewer.ipython.org/github/bokeh/bokeh-notebooks/blob/master/index.ipynb
[solarmonitor]: http://solarmonitor.org/
[skimage]: https://github.com/jni/skimage-tutorials/tree/euroscipy2015/2015-euroscipy
[skimage-tutorials]: https://github.com/scikit-image/skimage-tutorials
[sklearn]: http://scikit-learn.org/
[cambridgecoding]: http://www.cambridgecoding.com
[sklearn-practice]: https://github.com/cambridgecoding/euroscipy-tutorial
[stats-tutorial]: http://gaelvaroquaux.github.io/stats_in_python_tutorial/
[pandas]: http://pandas.pydata.org/
[statsmodels]: http://www.statsmodels.org/
[cython]: http://cython.org/
[cython-tutorial]: http://nbviewer.ipython.org/url/consulting.behnel.de/esp/2015/EuroSciPy2015.ipynb
[numba]: http://numba.pydata.org/
[greg]: http://third-bit.com/
[software-carpentry]:
[swc-training]:
[how-learning]: https://books.google.co.uk/books?id=gu5qpi5aFDkC
[building-better]: https://books.google.co.uk/books?id=cPLEoQEACAAJ
[multichoice]: https://etherpad.mozilla.org/wDt3F4I5hv
[swc-reading]: http://swcarpentry.github.io/training-course/materials/
[tdd]: https://en.wikipedia.org/wiki/Test-driven_development
[hintjens]: http://hintjens.com/
[Whintjens]: https://en.wikipedia.org/wiki/Pieter_Hintjens
[0MQ]: https://en.wikipedia.org/wiki/%C3%98MQ
[0MQOreilly]: https://library.oreilly.com/book/0636920026136/zeromq/toc
[0MQguide]: http://zguide.zeromq.org/
[Wstalin]: https://en.wikipedia.org/wiki/Joseph_Stalin
[wikipedia]: https://en.wikipedia.org/wiki/Wikipedia:About
[ianozsval]: http://ianozsvald.com/
[elevate]: http://elevatedirect.com/
[textract]:https://textract.readthedocs.org
[tika]: https://tika.apache.org/
[cermine]: http://cermine.ceon.pl/index.html
[turkishI]: http://haacked.com/archive/2012/07/05/turkish-i-problem-and-why-you-should-care.aspx/
[diedot]: http://gizmodo.com/382026/a-cellphones-missing-dot-kills-two-people-puts-three-more-in-jail
[glueviz]: http://www.glueviz.org/
[seaborn]: http://stanford.edu/~mwaskom/software/seaborn/
[Alchemy]: http://www.alchemyapi.com/
[DBPedia]: http://wiki.dbpedia.org/
[ian_slides]: https://speakerdeck.com/ianozsvald/data-cleaning-on-text-to-prepare-for-analysis-and-machine-learning-at-euroscipy-2015
[JuanTalk]: https://github.com/jni/streaming-talk
[pytoolz]: https://github.com/pytoolz
[read_pytoolz]: http://matthewrocklin.com/blog/work/2013/10/17/Introducing-PyToolz/
[read_wordcount]: http://matthewrocklin.com/blog/work/2013/11/15/Functional-Wordcount/
[MikaelTalk]: http://slides.com/mikaelmortensen/massively-parallel
[klepto]: https://github.com/uqfoundation/klepto
[pyMIC]:
[pyFR]:
[JyNI]:
[Jython]:
[dask]: http://dask.pydata.org/en/latest/
[gr]: http://pgi-jcns.fz-juelich.de/pub/doc/EuroSciPy_2015/00-talk/assets/player/KeynoteDHTMLPlayer.html
[matplotlib]: http://matplotlib.org/
[flexx]: http://flexx.readthedocs.org/en/latest/
[Spimagine]: https://github.com/maweigert/spimagine
[Olivia]: https://github.com/oew1v07
[skimage-1650]: https://github.com/scikit-image/scikit-image/issues/1650
[skimage-1673]: https://github.com/scikit-image/scikit-image/pull/1673
[skimage-1659]: https://github.com/scikit-image/scikit-image/pull/1659
[datajoy-1659]: https://www.getdatajoy.com/project/55e192d061caf1ed47d39dd3
[datajoy]: https://www.getdatajoy.com/
[jupyter-washington]: http://faculty.washington.edu/rjl/notebooks/
[nbgader]: http://nbgrader.readthedocs.org
[sagemath]: http://cloud.sagemath.com
[rwilson]: http://www.rtwilson.com/
[recipy]: https://github.com/recipy/recipy
[CWblog]: {% post_url /2015/04/2015-04-02-Amazing-workshop %}
[pyastroblog]:{% post_url /2015/04/2015-04-26-PythonAstronomy %}
[ReScience]: http://rescience.github.io/
[holoviews]: http://holoviews.org/
[kwant]: http://kwant-project.org/
[drugstalk]: http://mnowotka.github.io/presentations/euroscipy/
[plyadestalk]: http://nbviewer.ipython.org/github/helgee/euroscipy-2015/blob/master/Plyades%20Demo.ipynb
[fliestalk]: http://damcb.com/gathering_thoughts.html
[probprogramming]: http://slides.com/springcoil/probprogramming
[astropy]: http://astropy.org
[whnp]: http://www.womenhackfornonprofits.com/
[pycharm]: https://www.jetbrains.com/pycharm-educational/
[sklearn_gallery]: http://scikit-learn.org/stable/auto_examples/index.html
[citation]: http://blog.rtwilson.com/encouraging-citation-of-software-introducing-citation-files/
[posterwinner]: https://www.openstreetmap.org/search?query=erlangen
[osm_erlangen]: https://www.openstreetmap.org/#map=11/49.5985/11.1233