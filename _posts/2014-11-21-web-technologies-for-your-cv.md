---
layout:     post
title:      "Web Technologies for Your CV"
categories: technology
excerpt: >
    I really like web technologies. But... would they be appropriate for
    writing a CV?
---

Faced with the need to update my CV, I pondered the possible toolchains:

- My previous CV was written using *LibreOffice.* This worked fairly well, even
  though it lacked coolness and precise control over the layout.
- Many colleagues use *LaTeX* (shudder).
- My flatmate suggested that I use a *plain text file.*

I found the last option intriguing. I really like plain-text files, especially
in combination with light-weight markup such as
[MarkDown][md]. This is the technology behind the blog
you're reading; it works very well for web publishing. Tool support for editing,
version control etc. is great... but would it be appropriate for writing a CV?

It turns out that today's web developers have great control over how websites
are printed. CSS properties can control font families and weights, page margins
and breaks, and even typographic features like columns, soft hyphens, or orphan
lines. After a bit of reading on this, I assembled my toolchain:

1. `git init .` is a standard command to execute at the beginning of a new
   project.

2. Using [LibreOffice][libreoffice] and [Pandoc][pandoc], I converted my old CV
   from `.odf` → `.docx` → `.md`. This was a great starting point.

3. [Vim][vim] is my tool of choice for editing the MarkDown file.

4. After I was done updating the CV, I converted it to HTML using Pandoc. The
   tool allows its users to control every aspect of the document template being
   used, and also contains a lot of options to make the appearance nicer (e.g.,
   turning apostrophes into typographic quotes).

5. The result looked basic, but all the content was there. Time for some
   styling! I started by adding [normalize.css][normalize], and then adjusted
   the style sheet until the document satisfied my gusto.

   Most of the styling was done with the HTML document open in [Chrome][chrome].
   For those features that were related to document layout, I used the print
   preview to see the effect of the changes.

   It's noteworthy that the process is much more WYSIWYG than one might think,
   because CSS properties can be adjusted dynamically using Chrome's developer
   tools.

5. Time to convert the document to PDF! Chrome's print-to-PDF and the Quartz
   renderer did a good job. They even preserved hyperlinks, so that readers can
   open referenced websites directly from their PDF reader.

6. The last missing point is PDF metadata. It would be nice if the author and
   subject of the document were set correctly. Enter [PDFTK][pdftk], which
   performs a final pass over the PDF file to update these fields. 

Here's [the resulting CV][cv]. What do you think about it? Feedback is very
welcome. Internships too... please refer to my CV if you're interested :)

I also made the [source code of the CV][cv_source] publicly available. If you'd
like to see the CSS styles or Pandoc command line options, this is the place to
go. I hereby publish it under the Creative Commons Attribution-ShareAlike 3.0
license; share, tweak, use, and enjoy!

[md]: http://commonmark.org/
[libreoffice]: https://www.libreoffice.org/
[pandoc]: http://johnmacfarlane.net/pandoc/
[vim]: http://www.vim.org/
[normalize]: https://necolas.github.io/normalize.css/
[chrome]: https://www.google.com/chrome/browser/
[pdftk]: https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/
[cv]: /assets/documents/cv_jonas_wagner.pdf
[cv_source]: https://github.com/Sjlver/cv
