---
title: 'LaTeX: How to cite URL'
date: 2018-01-29 17:25:27
tags: LaTeX
categories: LaTeX
---


LaTeX is powerful and useful paper editor and document preparation system for Microsoft Word. You can use LaTeX to make elegently prepared papers.

Today's question is how to use BibTeX to cite URL, the following is my solution

* use package url

```shell
\usepackage{url}
```

* add the bibtex of URL to `.bib` file

```shell
@Misc{example.com,
howpublished = {\url{http://example.com/myexample/}},  
note = {Jan 29, 2018},
title = {My Title},
author = {Jackson, Jenkens and Mike Nielson}
}
```


