---
layout: post
title:  " $\\LaTeX$ Cheatsheet"
date:   2016-04-24 20:38:59 +1000
categories: latex
permalink: latex-cheatsheet
---
> _Note: This is a live document. It will be updated regularly as I find new tricks in using $\LaTeX$._

### Inserting tables

It's a daunting task to insert tables in $\LaTeX$. Fortunately, I found one of the easiest way to insert a table in $\LaTeX$ documents is to use csvsimple package.

{%highlight latex%}
\usepackage{csvsimple}
{% endhighlight %}

The usage of this package is pretty simple. Just follow the following example:

{%highlight latex%}
\begin{table}
	\csvautotabular{<filename.csv>}
	\caption{insert_your_caption}
	\label{insert_your_label}
\end{table}
{% endhighlight %}

It's very convenient because we don't need to convert the CSV into $\LaTeX$ table formatting (which is, I found, frustrating). Thanks to [this website][csv-simple] for the insight of how to do this properly.

### Inserting graphics

If you ever need to insert a graphic (which is I believe many times the case), use the graphicx package. Refer to the following example on how to do it properly:

{% highlight latex %}
\usepackage{graphicx}
\graphicspath{path/to/img}
...
\begin{figure}
	\includegraphics{graphics_file_name_without_extension} % usually PNG file
	\caption{caption_of_the_graphics}
	\label{label_of_the_graphics}
\end{figure}
{% endhighlight %}

The more complete guide please go to this [amazing webpage][latex-image].

##UPDATE 25 APR 2016##

### Creating bibliography

This particular part is very tricky in my opinion. I spent about 2 hours just to tweak and made it work appropriately. There are several options
for building the biblingraphy, e.g.: bibtex, biblatex, and several others. Honestly, I don't really know the difference between them, but from a little bit research, biblatex is one of the most common package that people use now as it provides more options.

#### Setting up the package

To use biblatex, there are several package to include:

{% highlight latex %}
\usepackage[utf8]{inputenc}
\usepackage{csquotes}
\usepackage[english]{babel}
\usepackage[backend=biber, style=trad-abbrv, defernumbers=true]{biblatex}
\addbibresource{<bibliography_file.bib>}
{% endhighlight %}

#### Preparing the .bib file

The `addbibresource` is to include the the .bib as the main bibliography file. The following sets an example of a .bib file:

{% highlight bib %}
@article{mohammad14,
	author 	= "Mohammad, Rami and Thabtah, Fadi Abdeljaber and McCluskey, T.L.",
	year 	= "2014", 
	title 	= "Predicting phishing websites based on self-structuring neural network",
	journal = {{Neural Computing and Applications}}, 
	volume 	= "25",
	number	= "2",
	pages	= "443--458",
	ISSN	= "0941-0643"
}

@article {mohammad14wc,
	author 	= "Mohammad, Rami and McCluskey, T.L. and Thabtah, Fadi Abdeljaber",
	year 	= "2014", 
	title 	= {{Intelligent Rule based Phishing Websites Classification}},
	journal = {{IET Information Security}}, 
	volume 	= "8",
	number	= "3",
	pages	= "153--160",
	ISSN	= "1751-8709"
}

@online {kerstein,
	author 	= "Kerstein, Paul L.",
	title 	= {How Can We Stop Phishing and Pharming Scams?},
	url		= {https://web.archive.org/web/20080324080028/http://www.csoonline.com/talkback/071905.html},
	urldate	= {2016-04-01}
}    

@online {lichman13,
	author = "Lichman, M.",
	year = {2013},
	title = {UCI Machine Learning Repository},
	url = {http://archive.ics.uci.edu/ml},
	urldate = {2016-04-01},
	institution = "University of California, School of Information and Computer Science"
}

@article {mohammadfeatures,
	author 	= "Mohammad, Rami and Thabtah, Fadi Abdeljaber and McCluskey, T.L.",
	title = {{Phishing Website Features}},
	year = {2015},
	url = {http://archive.ics.uci.edu/ml/machine-learning-databases/00327/Phishing%20Websites%20Features.docx},
	urldate = {2016-04-01}

}

@online { phishingreport,
	title = {{APWG Phishing Attack Trends Reports}},
	url = {http://www.antiphishing.org/resources/apwg-reports/},
	urldate = {2016-04-02}
}

@inproceedings{dharmaadi2014typo,
  title={Typo-squatting crime in Indonesia online banking},
  author={Dharmaadi, I and Bakhrun, Akhmad and Saputra, Dedi and Putra, Achmad Muchlis Abdi and others},
  booktitle={Information Technology Systems and Innovation (ICITSI), 2014 International Conference on},
  pages={269--272},
  year={2014},
  organization={IEEE}
}
{% endhighlight %}

There are several tags for that can be used, the above examples are some of them. `@article` is used to include an article within the bibliography, `@online` is used to include a webpage or other online materials. And so on. (For a more complete guide, visit [this website][biblatexref1] and also [this website][biblatexref2]).

Another important point to note in building the .bib file is how to write the authors. If there are more than one author, separate the names with `and` word (not a `,`). The name format can be `lastname, firstname` or `firstname lastname`. But the important thing is to separate them with the `and` keyword. (Refer to [this webpage](http://www.tex.ac.uk/FAQ-manyauthor.html)).


#### Printing the bibliography

For printing the bibliography in the document, use this following line:

{% highlight latex %}
\printbibliography[title={Bibliography}, heading=bibnumbered]
{% endhighlight %}

The `title` and `heading` options are optional. `heading=bibnumbered` is used if you want to have section number for the reference (it will following the order of section numbering). The `title={Bibliography}` option is used if you want to change the caption of the heading. The default caption is "References". (For more details, please [visit this website][printbibliography]).

#### Compiling the .bib
This step is one of the trickiest. Somehow I need to compile several times to make it work correctly. One thing that you need to remember is to have the correct sequence of build order:

1. pdflatex
2. biber
3. pdflatex

`pdflatex` command is just a normal build. But, if there's an error message asking to compile the biber, then use `biber` command. This is how you use the `biber` command in the Mac terminal (sorry, I'm using MacOS. Not really sure how to do it on other machines):

```
biber <tex_name_file_without_extension>
```
That's as easy as that. (But I spent more than 2 hours to solve this effin' stuff).

### Dealing with negative numbers

If you just put normal negative numbers, e.g.: `-2`, in your $\LaTeX$ document, the negative sign is treated as a hyphen (i.e., a sign that you can break in that particular position for a new line). To make it be treated as a negative sign instead of a hyphen, use this following trick:

{% highlight latex %}
\usepackage{siunitx}
\sisetup{
   detect-mode,
   detect-family,
   detect-inline-family=math,
}
...
\num{-2} % treated as negative sign
{% endhighlight %}

The source is [this website](http://tex.stackexchange.com/questions/79141/is-there-a-designated-symbol-for-the-negative-sign-in-say-16).


[csv-simple]: http://texblog.org/2012/05/30/generate-latex-tables-from-csv-files-excel/
[latex-image]: https://www.sharelatex.com/learn/Inserting_Images
[biblatexref1]: https://www.sharelatex.com/learn/Bibliography_management_with_biblatex
[biblatexref2]: https://www.sharelatex.com/blog/2013/07/31/getting-started-with-biblatex.html
[printbibliography]: http://tex.stackexchange.com/questions/134958/how-to-format-bibliography-titles-as-section-subsection-and-subsubsection
