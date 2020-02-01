---
title: Learning LaTeX
date: 2018-08-05 20:51:24
tags: LaTeX
categories: LaTeX
---

LaTeX is a stunning editor tool for writing academic papers, this post contains some LaTeX tricks. Updating . . .

###  Sepecifying any date using \date

Using `\date{}` can specify the date, for example `\date{August 6, 2018}` and it stores the date for later use and it would not show date on the page, insert it in the document by 

```
\makeatletter
\@date
\makeatother
```

And also you can use `\today` to insert the today's date into the document.
