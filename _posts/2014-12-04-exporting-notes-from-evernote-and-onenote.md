---
layout:     post
title:      "Exporting notes from Evernote and OneNote"
categories: technology
excerpt: >
    Evernote and OneNote are useful. But, can you get your data out of them if
    you have to? This post shows how.
---

Evernote and OneNote are useful. But, can you get your data out of them if
you have to? Consider the scenario where you would like to store your notes in a
set of text files. How would you get your existing notes out of the cloud and
into these files?

## Syncing Evernote

Evernote is supported by an online service called [CloudHQ][cloudhq]. This
service promises to synchronize data across a number of cloud providers. For
example, it can synchronize Evernote notes to a GDrive folder, which is what
we're going to use.

Once you've logged into CloudHQ, it lets you set up *synchronization pairs*. For
my pair, I choose Google Drive as the first service. CloudHQ prompts me to
log in to my Google account and authorize the access. Then, it allows me to
select a folder to use for the synchronization.

The second end of the synchronization pair is Evernote. Again, CloudHQ prompts
me to log in to Evernote and authorize the access. I can also select which
notebooks to sync.

Once the endpoints are set up, I can choose a number of options. The most
important ones specify the export format. I can choose between a Google doc, a
Word or LibreOffice doc, a plain text file, PDF, HTML, or Evernote's ENEX
format. Documents and plain text files can be synced back to Evernote, whereas
PDF or HTML are export-only formats.

## Syncing OneNote

The process is a bit more complex for OneNote, because it is not (yet) supported
by CloudHQ. However, OneNote does have an experimental REST API that lets you
access the notes.

For non-technical readers: a REST API is a wonderful thing. It is a way to
access data that is easy for programs to navigate. In the case of OneNote, the
API provides a way to fetch a list of pages, and to get the title, notebook name,
section name, and content for every page.

I've written [a small program][onenote_export] that accesses the API, downloads
all the notes, and stores them in a folder hierarchy that mimics your notebooks
and sections.

It's open-source, and suggestions are welcome. One known limitation is that the
program does not handle attachments. If your notes contain images, PDF files, or
other additional data, they will not be fetched. Let me know if you use the
program and would like to have this feature.

## Where To Go From Here

Once you have your notes as a set of local files, [Pandoc][pandoc] is a
fantastic tool to convert them to the format of your choice. It generates very
readable output (e.g., in the Markdown format) from a variety of inputs
(including HTML and Word documents).

## Conclusion

All these cloud services sometimes make you wonder: "Am I loosing control over
my data?" I guess we do, indeed. But sometimes, there is an API that allows you
to access your data in a programmatic way, and re-gain some of the control. If
you're a user, looking for such APIs and knowing how to use them can be very
helpful. If you're a developer, remember to build a public API for your
services; communities will form around them, people will start building plugins,
and your service won't be an isolated cloud, but part of the web. 


[cloudhq]: https://www.cloudhq.net/
[onenote_export]: https://github.com/Sjlver/onenote-export
[pandoc]: https://johnmacfarlane.net/pandoc/
