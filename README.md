# `usewhat`: what application or tool should I use to do this command line task?

Right now, this file is a sort of brainstorm although I am aware that ultimately this is not the purpose of a readme. 

## goal

This is a start of a project intended to aosle a problem I have still after quite a long time of using the command line:

* There are an overwhelming number of command line tools
	
* Many of them do similar things slightly differently

* It's difficult to remember which tool to use in which situation
 

## other ways to solve the problem that don't work for me

* **tldr** - Once you know what to use, [tldr.sh](https://tldr.sh/) is a great tool to help quickly remember *how* to complete many common tasks. This is intended to be the step *before* `tldr`. 
	
* **look it up on the internet** - I find myself re-researching the same things over and over again just trying to remember "what was that tool called?" which is a waste of time. At a certain point there is no more learning. 
	
* **take notes** - the notes became hard to manage because there were so many of them; this project is intended to help focus th enote taking to the bare essentials by providing significant constraints.
	
* **look in your history file** - once you have done something a bunch, assuming you have continuous access to the same history file and you can recall enough context, it *is* useful. If these conditions are not met it becomes difficult or impossible. Additionally it relies on having strong command of search tools to sift through it, and search tools are a category I find very confusing to remember about. 
	
* **`apropos`** - a component of GNU's [https://www.gnu.org/software/gnuit/](`gnuit`) is to my knowledge the primary existing attempt to fill this need. I have not found it useful when I've tried it  because the information it spits out seems to be automatically collected from various sources without any editing. My attempts at using it have filled the screen with lots of junk. This project seeks to be more careful and concise. There is a package called [`apropos2`](http://www.georgeanelson.com/apropos2.htm) which honestly I haven't tried as like the original I don't think it has been updated in quite a while. 

## how it could be done

### file format for data storage

Since I don't know how to do anything, I will try with a few files to see if I can figure out how to make them work. I am thinking to use `yaml` to store the data. I have use `yaml` before and it is reasonably useful. It will be easier for me to manage than alternatives I considered

* overkill formats I decided against: `xml`, `json` and `mysql`. these offer too many opprotunities to foul things up and get lost in the weeds. 

* formats that are too simple for my needs: `text`, `markdown` (used by `tldr.sh`), `csv`. 

### approximate data structure

looking at `tldr.sh` I see they have every application as its own file. I think there are advantages to this rather than one large file, especially for managing in a git repo. 

* Easy to see what is available

* Easy to track changes

* compatible with `yaml` file format

* would allow specilized collections of tools for uncommon use cases to be added modularly

* since there are so many thousands of applications and I am thinking to keep the scope narrow, there could be different ideas about what to include; this would allow additional packages of files for those who want them, or fewer for those who want the basics

* could be used to make a web interface using a static site generator like `hugo`

As to the internal structure of the file, I plan on developing it as I go, iterating it slightly with each file and then after about a dozen or so, have a good plan as to what is required and what makes sense.

**TODO: Add an "alert" field.** Need a way to ensure communication of any common missteps, dangers or incompatibility that a tool could present.

### TODO: decide on a minimal number of feilds to be filled in order for a program's file to be included

I have included in the draft `yaml` structure so far a fairly comprehensive (if basic) structure for the data. But in order to be useful they need not all be filled. For example I have included programing language because it if relevant for some use cases but it is not really *Required*. In fact it might be useful to concentrate on having the list of programs be "complete" rather than every item being fully informed. This would at least let the user having a starting point for their documentation/web search if nothing else. 

Especially if included was an easy way to make contributions back to the repo; so information could be added as people are going along their way. 

### querying from the terminal 

At the moment I am thinking of using `ugrep` to do the actual work though that might change. There are a few different ways of directly accessing `yaml` files but then there would also be the option of converting them into something else for terminal use. 

## test of concept

To test this concept, do a set of search and finding tools

- [X] `find`
- [ ] `fd`
- [ ] `ag`
- [ ] `fzf`
- [ ] `tree`
- [x] `ls` 
- [ ] `locate`
- [ ] `grep` (`egrep`, etc)

	
other tools which will be excluded from the small text batch: `awk`, `sed`, `up`, `percol`, `rg`, `ack`, `pdfgrep`

And to make sure it will make sense outside a single category I will do approximately 6 more of other sorts of tools which are tbd.  

 - [ ] ? unknown #1
 - [ ] ? unknown #2
 - [ ] ? unknown #3
 - [ ] ? unknown #4
 - [ ] ? unknown #5
 - [ ] ? unknown #6
	
## other categories which are high priority for me

 * text editors
 * determining file/directory size
 * file copying, mirroring, archiving, backup
	* local
	* remote
 * compression, decompression
 * file managers
 * navigating filesystem (`cd`-like)
 * help (`tldr`-like)
 * the basic text manipulation tools (`cut` etc)
 * tools that are modern replacements for classics (`bat` for `cat` etc)
 * shells - might be too complicated
 * in-shell features (can't recall the name for these) like `>`, `tee` etc
 * file/directory watching utilities (`inotify`)
 * basic automation (`cron`)

## limitations: categories it might make sense to skip for now

I think the below would be useful but perhaps as a "module" or something that someone else would like to take on caring for; beyond me to look after.

### development tools

 * VCS and realted, eg `git` and the thounsads of tools that have been created for it
 * scripting langages (*very* basic; or not at all)
 * debuggers
 * environment managers (for running pythons, rubys etc)
 * add-ons for text editors (`vim`, `emacs` etc)

### self hosting, servers

A whole category of complex tools. 

### niche needs and use cases

There are many things the terminal can be used for but this project for the time being will focus on the fundamentals that most people could ebenefit from and that can be combined with all kinds of tools according to the [Unix philiosphy](https://en.wikipedia.org/wiki/Unix_philosophy).

* task management
* email
* web

## edge cases: would like to have but I probaly can't manage

### system level utilities

While I think a full description of the utilities a sysadmin would use in a professional environment would be well outside the scope of this (and I'm sure someone in that role wouldn't care for this kind of info anyway) there are some basics that would be helpful, like those involving logging. 

However this could get complicated with different architechtures. 

# Enhancements (wishlist)

## auto customize result to environment

### discriminate between what's installed and what's not

Would be great if it was able to detect if tool is installed. So when searching for a a tool to do a certain job, could either 

 * limit to already-installed tools, or
 * display tools which are not available in a visually-distinct style such as italics or as a seperate list

### detect available package managers and suggest install options

 * determine what package manager (`apt`, `yum` etc) I am using and suggest install line. 
 * even better: interface with that package manager to check if it exists in repo
 	* what version is available?
 	* is this the most up-to-date version?

#### using other package managers
 * some tools are available via 3rd party package managers such as `pip`, `cargo`, etc
 * depending on local package manager, this may be the only way they are available, or there may be a more up-to-date version available that way compared to package manager
 * detection of what extra package maangers are available and suggest install options might be desireable
 * on the other hand, might be well out of scope considering desire to keep things "simple" at least for the time being


# resources: 

* [List of GNU packages - Wikipedia](https://en.wikipedia.org/wiki/List_of_GNU_packages)

















