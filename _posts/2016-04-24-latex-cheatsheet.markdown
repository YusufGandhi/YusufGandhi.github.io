---
layout: post
title:  "LaTeX Cheatsheet"
date:   2016-04-24 20:38:59 +1000
categories: latex
---
### $\LaTeX$ Cheatsheet

#### Inserting a table

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

#### Inserting a graphic

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

[csv-simple]: http://texblog.org/2012/05/30/generate-latex-tables-from-csv-files-excel/
[latex-image]: https://www.sharelatex.com/learn/Inserting_Images
