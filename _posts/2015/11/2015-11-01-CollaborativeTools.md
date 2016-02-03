---
layout: post
title:  "Colaborative tools"
date:   2015-11-01
time:   "17:30:00"
blog:   "true"
categories: ["collaborations", "community"]
---

List of collaborative tools I've used or I've heard of. 
This list will be update regularly as I found new tools.
The update date will be added at the end.

If you know of other tools, please, let me know about them and
I will add them in here.
<br></br>

## Sharing files
 - [Dropbox][dropbox]
 - [Google drive][gdrive]
 - [One Drive][onedrive], microsoft's solution.
<br></br>

## Real-time editing
 - [Google docs][gdocs] for a full office suite
 - [etherpad][etherpad] for plain text
    - [sandstorm][sandstorm] also offers etherdraw, ethercalc,...
    - [framasoft][framasoft] has a version of the above (but in French).
 - LaTeX or similar editors
    - [Overleaf][overleaf] what used to be writelatex. Free up to 1GB.
    - [ShareLaTeX][sharelatex], an open source LaTeX editor that can be used on their site or installed in a personal server. Also available as [Sandstorm][sandstorm] app.
    - [\BlueLaTeX][bluelatex], another open source LaTeX editor backed by [Mozilla Science Lab][bluelatex_moz]. Needs to be installed in server.
    - [Authorea][authorea], really easy to use editor aimed for researchers to upload papers directly to some journals. You can write comments/discuss on a particular paragraph.
    - [Cloud.sagemath][cloudsagemath], a cloud based environment which has a terminal, file system and more: a full scientific linux box in the cloud (R, Python, LaTeX etc...).
<br></br>

## Collaborative editing documents
 - Wiki software
    - [MediaWiki][mediawiki], the software that runs wikipedia.
    - [Federal wiki][fedwiki], the revamp of the origin of the wikis. Fancy interface.
 - Track changes on office suites
    - Microsoft Office, LibreOffice and others have a track changes capability useful when
      sharing the same file (eg. through dropbox, shared disk or email).
<br></br>

## Collaborative editing code
  - Version control software
    - [git][git_site] is the one developed by Linus Tovarlds
    - [mercurial][hg_site] seems quite easy to learn (I haven't used it yet).
    - [Baazar][baazar_site], subversion (svn), cvs, and [many more][w_versioncontrol]
    are available.

  - Version control platforms
    - [GitHub][github] offers a great way to do code-review.
    - [bitbucket][bitbucket]
    - [GitLab][gitlab] is an open-source github clone. You can install it in your servers.

  Version control is great for plain-text, but many use word like documents, or
  spreadsheet, or Ipython notebooks. Some solutions for that is:
    - [nbdiff][nbdiff] is a diff viewer for jupyter-notebooks.
<br></br>

## Pair programming
  - [MadEye][madeye] is a real-time code editor that can be used through Google hangouts
    or independently.
  - [Codebox][codebox] to code in the cloud.
  - Plugins for GitHub's text editor [atom][atom] allows pair-coding
     - [AtomPair][atompair]
     - [motepair][motepair]
  - [Sense][sense] a paid platform for Python, R, Julia and Spark
  - [DataJoy][datajoy] like the above with a free plan, made by the [ShareLaTeX][sharelatex] people. Check this [example][datajoy_scikitimage] of scikit-image gallery.
  - screen sharers/cast; not extrictly collaborative coding but helping others
    - [asciinema][asciinema] allows you to record your terminal as text.
    - [shellshare][shellshare] broadcasts your terminal.
    - [recordit.co][recordit] record your screen, share as gif or video.
<br></br>

## Communities
  - [kune][kune] a community environment using what it was once google wave and now
  kept by [apache][wave_apache]. It offers blog, wiki, document storage, chat, etc.
  Also it's possible to install it in your own server.
  - [Exo|tribe][exo_tribe], the open source version of the Exo platform. Provides forum,
  calendar, documents, etc.
<br></br>

## Share research steps
  - [Open Science Framework][osf] a github like interface for your data and experiments.
  I find it a bit difficult to understand.
  - [docollab][docollab] similar to the one above, I'm lost with protocols and plates.
  - [SubstormZoo][substormzoo] an online analysis platform for space weather data analysis
  includes notebooks and discussion boards with team members.
  - [myExperiment][myexperiment] is a [Taverna][taverna] (and others) online repository.
  Allowes groups and versioning of the workflows. Also provides metrics of who uses yours.
  It would be excellent if [OnlineHPC][onlinehpc] is collaborative.
  For now, e-infrastructures as [er-flow][erflow] or [shiwa][shiwa] builds on workflows
  so researchers can run some of them.
<br></br>

## Share results as papers
  - [Zenodo][zenodo] integrates with github and produces doi for your code, but also for
  other material like data, presentations, posters, lessons, etc.
  It's powered and funded by [CERN][cern], EU and [OpenAIRE][openaire].
  - [figshare][figshare] is older than zenodo but it's original moto is share data,
  negative results too!
<br></br>

## Sharing References
  - Mendeley, started independent but now belongs to Elsevier. It has a social-network
  system that allowes you to follow researchers and a recommendation system based on your
  library.
  - zotero, independent and open source. You can install it in your servers.
  - ADS is for searching, but I've heard that it may be possible in the near-future to share
<br></br>

## Linkedin like for Researchers
  - Research Gate
  - Academia
  - ImpactStory
  - Google scholar, with similar profil
  - Author labelling
    - OrcID, independent
    - ResearcherID (Thomsom Reuters; Web of Science)
    - Author Identifier (Elsevier; Scopus)
    - SPASE registry (space science)
<br></br>

## Chating and discussion systems
  - Video included
    - google hangout
    - skype
    - webex
    - GoToMeeting
    - jitsi; Open source
    - tux; encrypted
  - Text based
    - IRC, the classic, with endless extensions and bots.
    - gitter
    - slack, allows to add people and see history, also to add documents and hook to
    other systmes.
    - [There are software][sameroom] that helps to connect between different chat systems.

[dropbox]: http://dropbox.com/
[gdrive]: https://drive.google.com/
[onedrive]: https://onedrive.live.com/about/en-gb/
[gdocs]: https://docs.google.com/
[etherpad]: http://etherpad.org/
[sandstorm]: https://apps.sandstorm.io/
[framasoft]: http://framasoft.net/
[overleaf]: https://www.overleaf.com/
[sharelatex]: https://www.sharelatex.com/
[bluelatex]: http://www.bluelatex.org/
[bluelatex_moz]: https://www.mozillascience.org/projects/gnieh-bluelatex
[authorea]: https://www.authorea.com/
[mediawiki]: https://www.mediawiki.org/wiki/MediaWiki
[fedwiki]: http://fed.wiki.org
[git_site]: http://git-scm.com/
[hg_site]: https://www.mercurial-scm.org/
[baazar_site]: http://bazaar.canonical.com/en/
[w_versioncontrol]: https://en.wikipedia.org/wiki/Comparison_of_version_control_software
[github]: https://github.com/
[bitbucket]: https://bitbucket.org/
[gitlab]: https://about.gitlab.com/
[nbdiff]: http://nbdiff.org/
[madeye]: https://madeye.io/
[codebox]: https://www.codebox.io/
[atom]: https://atom.io/
[atompair]: https://blog.pusher.com/atom-pair/
[motepair]: http://motepair.github.io/motepair/
[sense]: https://sense.io
[datajoy]: https://www.getdatajoy.com/
[datajoy_scikitimage]: https://www.getdatajoy.com/project/55e192d061caf1ed47d39dd3
[asciinema]: https://asciinema.org/
[shellshare]: http://shellshare.net/
[kune]: http://kune.cc/
[wave_apache]: https://incubator.apache.org/wave/
[exo_tribe]: https://community.exoplatform.com/portal/intranet/
[osf]: https://osf.io/
[docollab]: https://www.docollab.com/
[substormzoo]: https://www.substormzoo.org/
[myexperiment]: http://www.myexperiment.org/
[taverna]: http://taverna.incubator.apache.org/
[onlinehpc]: http://onlinehpc.com/
[erflow]: http://www.erflow.eu/
[shiwa]: http://www.shiwa-workflow.eu/
[zenodo]: https://zenodo.org/
[cern]: http://home.cern/
[openaire]: https://www.openaire.eu/
[figshare]: http://figshare.com/
[sameroom]: https://sameroom.io/open-a-tube
[cloudsagemath]: https://cloud.sagemath.com/
[recordit]:http://recordit.co/


<!-- http://www.nature.com/news/online-collaboration-scientists-and-the-social-network-1.15711 to read -->
