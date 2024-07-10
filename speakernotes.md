# How to Create a LaTeX Report Without Losing Hair
Eirian Perkins
RezBas 2024

(show speaker notes during presentation)

## Hour 1

# Introduction

- intro 
- I'm a LaTeX enthusiast (ok, maybe that's an understatement)
- my goal is to share all the tips I wish I had when I started my PhD
- I hope this is helpful

## Pre-Indtroduction

- What is LaTeX
    - LaTeX is a document preparation software system
    - widely used in academia
    - using LaTeX feels more like programming
- Why would I want to use it?
    - more control -- fine tune look and feel, use it with Git (version control), collaborate
    - distraction-free environment
    - stay tidy and organized
    - search all your notes and work quickly
    - once you know the tool, preparing a document is **FAST**

## Goals

In today's workshop, you will learn to...

- create an article or a book (thesis)
- manage references
- gain confidence debugging errors

## Caveats

- this is intended to be an intermediate-level workshop
- if you're not familiar with LaTeX, don't panic
    - ask questions instead!
    - this will help others
    - you will have all of the code, so you probably won't fall behind
    - it will be ok
- the template is a work in progress
    - I update it after getting feedback at ResBaz
    - You can help me improve it by asking for more examples

## Examples

- look at samples (compiled PDFs, e.g. solaR, PYR, minutes with Anna)
- intent: whet your appetite for learning
- (after this session, you'll have the skills to make documents like this yourself)

## Getting acquainted with Overleaf

- Nothing we're doing today requires overleaf
- But lots of people prefer using it
- And it's easier to get started
- if you don't want to use overleaf, we can catch up later
- for now, let's get started


Logging in 

- use your UoA login or, if you don't have one, create an account
  - (wait for everyone)
- New Project -> Upload Project -> upload a .zip file
  - go to `https://github.com/eopResBaz/ResBaz2024_LaTeX`
  - `download zip`
  - OS X - may have to turn it into a zip again

- (open document.tex if it didn't open automatically)
  - on the right hand side, you should see a preview of the document
  - Overleaf will compile the document for you
  - on the left hand side is the "source code"
  - the main doc should be open, and you should see the preamble
  - at a glance, you can see the structure of the document. It is simple



## Basic Structure of a LaTeX document
```
┌── preamble
└── body
```

- preamble is where you do your configurations
  - what kind of document do I want to make?
  - e.g. is it an article? is it a book? (`\documentclass`)
    - (we'll talk about article and book classes today)
    - (for now, just accept this example is a memoir)
    - (more info: https://tex.stackexchange.com/questions/208791/is-memoir-class-like-an-extended-version-of-book-class)
  - what "look and feel" do I want? How is it styled?
    - can I click on links?
    - what colours do I want?
    - what do my chapter headers look like?
  - you can split your settings into multiple files, if you like
    - these are typically .sty or style files
    - (look at template/eirianstyle.sty)
    - you don't have to know all the details here
    - more importantly, notice that it's clean and organized, 
      and that putting your configurations in a style keeps 
      your main document tidy, and lets you easily re-use 
      your settings in other documents
    - make sure to leave comments so you know what you're doing
    - it's easy to make a big mess otherwise
  - there's some other configurations in `document.tex`
    - glossary
    - text color

- after you set up the configurations, then you have the body
  - the meat of the work, the actual content
  - I like the cognitive distinction between formatting and content,
    because it helps me focus when I write. 
      - I find that \LaTeX{} helps provide a distraction-free environment
  - one reason writing docs in \LaTeX{} can go so much more quickly
    than in, say, MS Word. Your settings in the preamble will largely
    take care of the look and feel of the document, so you won't have
    a buttons and toolbars surrounding your work.
- you can import files for your preamble, rather than dumping
  everything into your main .tex document
    - (show the different files in the template, and how they 
      render in the PDF)
    - (uncomment the 00_timelinetemplate.tex file)
      - (show in the GUI where the source file is located)
      - (modify the timeline to add something personal)
- we also have appendices
  - just renumber the chapters
  - add an appendix page using `\appendixpage`
  - ...and Bob's your uncle
  - this is no different than what we did before with subfiles
    - (open any of the examples and show how they're structured)

## More complex structure
(We just looked at this!)
(walk through document.tex again)

```
┌─┬─ preamble
│ ├─┬─ document class
│ │ ├─── article
│ │ ├─── book
│ │ └─── memoir
│ └─── style
└─┬─ body
  ├─── title
  ├─── ToC
  ├─── main document
  ├─── appendices
  ├─── glossary
  └─── bibliography
```

We don't have an example of a title. Let's make one

Try using `\maketitle` in the main document
- that didn't work
- what can we do?
- usually, I try using Google
- stackexchange has great information
  - https://tex.stackexchange.com/questions/122119/making-a-title-page-with-a-subtitle-in-memoir
  - what is the top answer telling us?
  - (create a macro in the preamble)
  - should it go in `document.tex` or `eirianstyle.sty`?

```
\newlength\drop
\makeatletter
\newcommand*\titleM{\begingroup% Misericords, T&H p 153
\setlength\drop{0.08\textheight}
\centering
\vspace*{\drop}
{\Huge\bfseries The Title}\\[\baselineskip]
{\scshape the subtitle}\\[\baselineskip]
\vfill
{\large\scshape the author}\par
\vfill
{\scshape \@date}\par
\vspace*{2\drop}
\endgroup}
\makeatother

\begin{document}

\begin{titlingpage}
\titleM
\end{titlingpage}
```

Scroll down just a touch, and we'll see a less complex solution,
and also see what went wrong with our `\maketitle` attempt

```
\title{The Title}
\author{All of Us}


\begin{document}

\begin{titlingpage}
\maketitle
\end{titlingpage}
```

Ok, continuing our re-cap:

```
┌─┬─ preamble
│ ├─┬─ document class
│ │ ├─── article
│ │ ├─── book
│ │ └─── memoir
│ └─── style
└─┬─ body
  ├─── title
  ├─── ToC
  ├─── main document
  ├─── appendices
  ├─── glossary
  └─── bibliography
```

Let's try generating a glossary
- (uncomment `\makenoidxglossaries`)
- (nothing shows, check glossary.sty)
- (change `key`, `name`, and `description`)
- (use `\gls{latex}` in the timeline and recompile)
- (add `\usepackage{pages/glossary}` to preamble)


---

## How are we feeling?

- make sense so far, at a high level?
- do you understand the structure of a LaTeX document?
- Good news:
  - we won't get any more complex than this
- Now we're going to work through some scenarios
  - OK if we don't get to all of them
- Any questions before we move on?
  - is everyone still able to compile?
  - (if not, suggest they create a new project and upload the zip again)


## Time check

Time for a break? Let's take 5
- (if it's been an hour already, take 10)

---

# Example 1


Scenario

- I'm a new PhD student and I have been given the task of performing
  a literature review

Goal

- create an electronic research notebook to log my progress
  - create a notes template for the articles I have read
  - `TODO: create a goals checklist to keep myself on task`
  - start populating it

First things

- what look and feel will we want?
  - decide if I want single column or multi-column
  - decide if I want a report (no chapters) or a book (chapter)
- create a new file for each section (page) I want to include
  in my report

`copy 00_pagetemplate.tex to 01_literature_notes.tex`

- comment out subfiles in main tex document
- we don't need these anymore, was just a preview of things to come
- add our new file `\subfile{pages/01_literature_notes.tex}`

In my head I'm thinking, how do I want to structure my document?
What sections will I need? We can think this through in our 
`document.tex` at a higher level, because we're including chapters
here rather than explicit content.

- I want a notes chapter to capture what I've learned about existing 
  work. I'll be able to refer back to my notes as I'm writing my
  manuscript. I can add citations as I go so that I don't need to 
  keep all my references and the sources that stood out in my brain.
- I have my own "convention" here 
  - templates start with `00` (or, in this demo, `01`, `02`, etc.)
  - new files, with real content, start with `YYYY-MM-DD`
  - this helps me distintuish between content and templates
  - ...and lets me see, at-a-glance what progress I've made to date

Open our new files for editing

## 01_literature_notes.tex

- let's think of what would be a good format for writing up our notes

document.tex
```
\documentclass[openany,onecolumn,oneside,english]{memoir}
```

- I've chosen a memoir class
  - this is like a book, it has chapters, sections, subsections,
    and so on.
  - after this workshop, you should have a play around 
    with other document classes to see what is possible
- the items in square brackets are documentclass options
  - you can specify papersize and format and so on.
  - `openany` refers to which hand side of a page a new chapter opens
    to. The default behavior is that chapters only open 
    on the right hand side.
  - `onecolumn` refers to how many columns are in our document
  - `oneside` refers to whether a document is single-sided or
    double-sided. Since I'm only viewing on the computer,
    one-sided looks more natural. Remember to change this for
    printing! You will leave enough space for the binding, which
    `twoside` helps with
- one thing to point out here
  - I make a conscious effort to document what the options I 
    select do. It is easy to forget and become disorganized.
    This is code. Document as a habit :) 


Now, to help us with our literature review, let's create a chapter 
template for notes on each of our references.
(modifying `01_literature_notes.tex`)

```
\documentclass[document.tex]{subfiles}
\begin{document}

\chapter{Literature Notes}

% make a template for each of my references
\section{template}

% summarize every article I've read
\subsection{Summary}

% questions specifically related to the article
\subsection{Questions}

% why is this relevant?
\subsection{How This Relates to my Research}

% Other important details
\subsection{New Vocabulary and Concepts}

\end{document}
```
(I got this idea from a lecturer I had in my master's program when 
he taught us how to read a research paper)


At this point, let's preview what our notebook looks like 

- demonstrate how to compile in Overleaf
- I have my ToC
- I have my literature notes
- Look at me, I have an appendix!

Do I need an appendix at this point? Probably not.

- let's try to remove our appendix ourselves 
  (not recommended for medical emergencies)
- `ask participants where to look`
  - has anyone been able to do this in overleaf?
- answer: in our main tex document

Remove the following:

- \appendixpage
  - the single page that says Appendices
- \label{appendixpage}
  - this is a label we can refer to when making clickable links
  - really great for referring to sections, figures, etc.
  - we need a label for creating a hyperlink
- \subfile{pages/0A_appendices.tex}
  - the actual appendix chapter we want to remove

Recompile, now the document is compiling as expected
- also demo, compiling a single page
- one shortcoming is the chapter number resets
  - we can make it a `\chapter*` for now


Alright, back to our template

- we decided we wanted to make a book, meaning we have chapters
  (unlike a report, that only goes up to sections)
- we created a new template file for each section
  - this will help getting us up and running quickly. 
    We can simply copy the template for each new reference
    we want to take notes on

Now that we have a template, I can demonstrate populating it

- first, we need to add a reference
- open `documentRef.bib`. It's in our main working directory
- we will be able to refer to a citation in any of our
  tex documents with a unique key. 
  - it's valuable to decide on a convention with naming
    keys. I believe this reduces my cognitive load when the
    key names are consistent and memorable
  - personally, I have an iPad where I do all my reading.
    How do I keep the documents I have there in sync with
    my bib document?
  - the way I do it is how I name my documents
  - first 3 letters of first author's last name
  - first 3 letters of second author's last name (if there is one)
  - and the year published
    - that's not always unique, so I may start adding  `a, b, c` 
      etc. to the end of keys
  - it took me a while to find a system that worked for me
    - I find this also works well with Zotero
    - if I need to use MS Word, I can import my .bib files 
      into Zotero natively, then when I search for a reference
      in Word, I can type the first 3 letters of the author's
      last name and the year, and it will come up
    - (demo importing a .bib file into Zotero)

```
@article{CabGar2013,
  author           = {Cabeller, Armando and Garc\'ia-Dorando, Aurora}, 
  title            = {Allelic Diversity and Its Implications}, 
  journal          = {The Genetics Society of America}, 
  volume           = {195}, 
  pages            = {1373-1384}, 
  doi              = {10.1534/genetics.113.158410},
  year             = {2013} 
}
```

author field

- `lastname, firstname and ...`
- there's no comma between author names
- `and` is the delimiter. This may be confusing initially
- the syntax for adding accented letters is a little funny
  - it's the same as LaTeX syntax
- my favorite reference for looking up accented letters
  - https://tex.stackexchange.com/questions/8857/how-to-type-special-accented-letters-in-latex

title

- the important thing to remember here is we need extra braces
  in order to get all caps
  - `{Allelic Diversity and Its Implications DNA}` will actually
    make DNA lower case, we need extra braces:
  - `{Allelic Diversity and Its Implications {DNA}}`

DOI

- remember to add this field
- omitting actual DOI here for brevity


```
@article{CabGar2013,
  author           = {Cabeller, Armando and Garc\'ia-Dorando, Aurora}, 
  title            = {Allelic Diversity and Its Implications}, 
  journal          = {The Genetics Society of America}, 
  volume           = {195}, 
  pages            = {1373-1384}, 
  doi              = {10.1534/genetics.113.158410},
  year             = {2013} 
}
```




Now, make a copy of our `01_literature_notes.tex` template

- e.g. 2024-07-11-CabGar2013.tex

```
\documentclass[document.tex]{subfiles}
\begin{document}

\chapter{Literature Notes}

\section{\citet{CabGar2013}}

\subsection{Summary}
fixation and differentiation are independent concepts

\subsection{Questions}
how can I learn all the maths
(is anyone laughing? are you all on mute?)

\subsection{How This Relates to my Research}
I want to investigate differentiation

\subsection{New Vocabulary and Concepts}

\end{document}
```

I will come back to new vocab in a moment, but first, I want to
do a preview

- if you get a questionmark for the section title, try 
  recompiling
- we can talk about changing the citation style later
  (this is different for natbib and BibLaTeX, depends on
  which tool you choose)

The thing is, it only tells me so much to have the author name
as the section title. It would be more informative if this instead
were the title of the work.

To figure out how to add this, I went to Google (as one does), and
Google told me to add 

```
\citetitle{CabGar2013}
```
 let's give that a go and see what 
happens...

- nothing meaningful shows up for my \citetitle command
- and I get a red X telling me `undefined control sequence`
- what the blazes does that mean?
  - we can click into `logs and output files` to learn more
  - `the control sequence at the end of the top line of your error message
    was never defined`

What we're being told, is that `\citetitle` doesn't exist. 
How is this possible? Did Google lie to us?

What's going on is, if we nip into our style file, we are using the package
`natbib`.

There's different packages for controlling our bibtex. 
I'm using `natbib` as an example here, why?
Because I was googling (as one does) to figure out how to 
add citations, and I found working examples.

This is a valid way to work through challenges in LaTeX.
But it turns out, there's multiple ways to accomplish 
a task, and sometimes I need to know a little bit more 
about what's happening "under the hood."

`natbib` is widely used. It's fast, and is a popular package.
However, it's not actively maintained, and has some limitations.
- great Q&A here
- https://tex.stackexchange.com/questions/25701/bibtex-vs-biber-and-biblatex-vs-natbib

More to the point, I don't know how I would pull out the title 
of a reference from natbib. So I want to use a different package.

Let's use `biblatex`, which does support the `\citetitle` command.

So taking a step back, when I went to Google, and I saw the 
recommendation for `\citetitle`, it was implicitly a recommendation 
for using `biblatex`.

- when we find answer on Q&A sites, we might be getting answers for 
  packages we're not using. So be aware of the requirements
- this advice will help you write professional reports without
  losing hair!!!
  
Let's use `biblatex`
  - remember anything in the curly braces is what you import
  - and anything in the square brackets are options
  - let's use `natbib=true` for compatibility with natbib
  - `style` has lots of options, for instance `apa`

```
\usepackage[style=numeric, natbib=true]{biblatex}
```

In the style file provided to you, you'll see I use the
`backend=biber` option. Biber is a replacement 
for the widely-used BibTeX software. 
 - It has expanded functionality and technical improvements 
   over BibLaTeX. For instance it offers
   full unicode support.
 - my personal recommendation is to use biber, but you might have 
   a good reason to use a different backend


Now that we've switched from `natbib` to `biblatex` we need to 
modify our `document.tex`. I have provided the necessary
`biblatex` commands in comments so that it's easy to 
switch out `biblatex` for `natbib`

- hint: search for `biblatex` in document.tex to find every 
  location that needs to be changed

Recompile, and check that we get the title as expected

---

## Ok, everyone take a deep breath

How we doing?


## Q&A

Let's pause for Q&A before taking a break

- anything you'd like more of?
- any questions?
- just press on after we finish?

## (stretch) Creating a TODO list

(if we don't have time, can cover in 2nd example)

Sometimes we'd like a feature that's not supported out of the box.
Let's suppose we want to create a TODO list, for setting goals and 
keeping focus.

- how can we create such a list?
- for me, a good first step is to google around and see if I can learn 
  what other people have done
- so, after some googling, I found this answer:
- https://tex.stackexchange.com/a/313337/153563

Modifying our style file

- We could copy the code and paste it in our document.tex preamble
- if we want to keep document.tex neat and tidy, a better place to 
  put this code is inside our style
- (actually, I have already done this for you)
- go to line 350
- I won't overwhelm you with the implementation details here, the 
  main point is that we can add commands and keep them tidy
- another important point is to leave yourself minimum working 
  examples (MWEs) so that you know how to use these commands
- I have shown this in the comments

Let's expand out our page template

```
\section{Daily Goals}
\begin{todolist}
  \item[\done] frame the problem
  \item write solution 
  \item profit
\end{todolist}
```

Or maybe we decided not to profit

```
  \item[\wontdo] profit
```

---

## Slower Glossary Example (as time permits)

Back to our 01_literature_notes.tex

```
\documentclass[document.tex]{subfiles}
\begin{document}

\chapter{Literature Notes}

\section{\citep{CabGar2013}}
\section{\citetitle{CabGar2013}}
\section{\citefield{CabGar2013}{journaltitle}}

\subsection{Summary}
fixation and differentiation are independent concepts

\subsection{Questions}
how can I learn all the maths
(is anyone laughing? are you all on mute?)

\subsection{How This Relates to my Research}
I want to investigate differentiation

\subsection{New Vocabulary and Concepts}

\end{document}
```

(choose one of the section titles to use)

Some other concepts

- making bulleted lists
- (compile example)

```
\subsection{New Vocabulary and Concepts}
\begin{itemize}
  \item{demes}
  \item{allelic differentiation}
\end{itemize}
```

we can also make enumerated lists:

- (compile example)
- these are built-in features
- unlike our `\todolist` which we implemented manually

```
\subsection{New Vocabulary and Concepts}
\begin{enumerate}
  \item{demes}
  \item{allelic differentiation}
\end{enumerate}
```

Now...

- Here I'm capturing new vocab and concepts
- ...but it would be great if I had a snapshot page that 
  gave me a summary of all of it
- Putting all of these concepts into a glossary would serve this purpose


Some background / rationale

- most examples I've seen online dump glossary definitions into the
  main tex preamble
- if we want to keep our `document.tex` neat and tidy, it would be
  better to have a dedicated file (or files) with 
  our glossary definitions.
- I placed my definitions into a `glossary.sty` file because that
  tells me, the file _must_ be imported in the preamble
- Note:
  - you may see other ways to set up glossaries
  - Consult the user manual to learn more, if you like: 
    https://mirror.aut.ac.nz/CTAN/macros/latex/contrib/glossaries/glossaries-user.html#tab:options

glossary set up

- `glossary.sty` is inside our `pages` directory
  - I know it's a style, but it made more sense to me, 
    cognitively, to put it in pages since it will 
    get print out later
  - recall: we put our other style inside template
- recall: in `document.tex` we did this:
```
\usepackage{pages/glossary}
```
- and also, at the end of the file, print the glossary by uncommenting:
```
\printnoidxglossary[nonumberlist, sort=word]
```

Next, open `glossary.sty`

```
\usepackage[toc,nopostdot,style=indexgroup]{glossaries}
% \glstoctrue adds glossaries to the table of contents
% use \glstocfalse otherwise
%
% nopostdot -- suppress the default post description dot
%
% style=indexgroup adds the letters above each section 

\glstoctrue
\makenoidxglossaries

\newglossaryentry{key}{
  name={The Name},
  description={
    The description of the entry
  }
}
```


Let's put our template entry back (see above).
This will make it easy to copy/paste new entries later

- I'm all about making templates so that I can copy/paste them later

```
\newglossaryentry{deme}{
  name={deme},
  description={
    a local group of individuals that interbreed with each other
  }
}
```

Now we can go back to our `01_literature_notes.tex` page and 
make our list of new vocab more interactive

```
\subsection{New Vocabulary and Concepts}
\begin{enumerate}
  \item{\gls{demes}}
  \item{allelic differentiation}
\end{enumerate}
```

`(should get an error)`

- ask participants what went wrong?
- some error about 'demes' has not been defined
- ... ?!?!
- change `demes` to `deme` and try again :) 

recompile

- now `deme` is clickable 
- (show off glossary page)
- (show off table of contents)
- may have to compile again for Glossary to show in ToC

table of contents

- notice that Glossary starts on page G1
- ...Bibliography starts on B1
- Let's take a peak at how we've done this -- it's not a default
  behaviour
- (`open document.tex`)
  - point out `\Renumber{G}`
- `\Renumber` isn't something that comes out-of-the-box with LaTeX
- I've defined it, it's in our `sty` file, so you can use it
  - let's take a peak
  - what I want to show you is, you can start making your own 
    macros
  - there's plenty of examples here, please have a play around
    and send me feedback after the session

How `\Renumber` works

- create a `\newcommand` taking `1` argument
- clear the page
- reset the page counter to 1
- make the new page start with whatever argument we've passed in
  - if we look again at `document.tex` we pass in letters
  - e.g. `\Renumber{G}`
  - look also at PDF preview ToC


Let's do one more glossary example

- I want to show off something I think is a common mistake
- (`open 01_literature_notes.tex`)

```
\subsection{New Vocabulary and Concepts}
\begin{enumerate}
  \item{\gls{deme}}
  \item{alldiff}
\end{enumerate}
```

- now reopen `glossary.sty` and add a definition

```
\newglossaryentry{alldiff}{
  name={allelic differentiation},
  description={
    The aspect of population structure relateing to Wright's 
    absolute differentiation.
  }
}
```

- (has everyone taken an intro to LaTeX?)
- (if not, I want to point out that if you add a linebreak 
  by pressing the enter key, it has no impact on the output.
  It just stops you from having one very very long line of text in 
  your editor. You need to add a blank line between lines of text
  for it to be meaningful to LaTeX, e.g. starting a new paragraph)


---

# Questions?

---

# Example 2

In our first example, we created a template we could use for a research
notebook or a thesis. 

- I emphasized creating templates that I can quickly copy and 
  modify
- The entire set-up we've seen is a template
- ...and we can create other kinds of documents with it

## Scenario 2

- I am a first year PhD student
- I want to record minutes for my supervisor meetings
  so that we can track my progress and reflect upon
  discussions and agreements
- I don't want to write a whole book for this!
  - Chapters don't really make sense
  - I want to give a 1 or maybe 2-page summary

Goal

- create a minutes template
- start populating it
- use a "draft" watermark until my 
  supervisor has had a chance to review the minutes

First steps

- how to re-use our template?
- use an `article` document class
  - articles don't have chapters
  - modify `document.tex`:
```
\documentclass[openany,onecolumn,oneside]{article}
```

- modify `00_pagetemplate.tex` 
  - remove `chapter`
  - replace it with `section` 
- copy `00_pagetemplate.tex` to `02_minutes.tex`
- only include `02_minutes.tex` subfile from main document.tex
- compile from `document.tex`
  - look for the red `X` errors (yellow `!` are warnings)
  - we need to fix these (remove the code, along with the ToC)
  - this is one thing I don't like about overleaf
  - ...it generates a PDF even if you have errors
  - if you built a PDF locally, the entire compilation would fail
- if you plan to share your LaTeX project with others, you 
  need to correct any errors that pop up. Be on the look out.

Now we are ready to start making our minutes template

## Minutes template

```
\documentclass[document.tex]{subfiles}
\begin{document}

\section{Minutes Template}

\end{document}
```

(mention I would copy to YYYY-MM-DD.tex) and start modifying:

```
\documentclass[document.tex]{subfiles}
\begin{document}

\section{Progress}
My ResBaz progress so far: we have completed the first activity.
The second activity is still in progress.

\section{Discussion}
I might not remember every detail from this session, but
now I understand how to structure my project so that it's tidy,
and I will try my best to read any error messages Overleaf shows me.

\section{Agreements}
I will have a go modifying this template after the session is over

\end{document}
```

I could reformat this document a bit, so that I can see my 
progress at-a-glance with a TODO list

```
\section{Progress}
\begin{todolist}
  \item[\done]  first activity
  \item second activity (in progress)
\end{todolist}

```


---


# Some other tips to prevent hair loss

- quotes -- ``quote'' versus "quote"
- no mathmode in references
  - (actually, this works in overleaf -- it shouldn't)
  - (will need to click into output log)
  - (always check for errors, they don't always pop up nicely for you)
  - .
  - try using \beta in a reference title
  - will get cryptic error message -- missing $ inserted
  - need \textbeta{} instead
- a tour of the `sty` file
  - main focus wasn't to go through every detail in here
    ...so I've mostly left it out of the tutorial
  - it's here for you to add on to
  - I try to keep it organized with little comment headers
  - you will thank yourself for leaving examples and comments 
    as you modify this file
- some cool stuff
  - the timeline template 
  - creating reference links
  - (be sure to add label)
  - combine these in an example...

```
\timeline{ResBaz}        {\nameref{chap:rezbas}}
```

- can go through template examples
  - listings
  - minted
  - table
  - subcaption




