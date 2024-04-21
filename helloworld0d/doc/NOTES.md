update: I'm having success converting to acmart latex format by using ChatGPT. Goal: to format a paper with the possibility of submitting it to OnWard! by Apr. 25.

I wrote the content in a WYSIWYG editor (Pages on MacOS). [I have lots of screenshots and want to see them in my editor as I write].

Then...

1. exported it to .docx format

2. $ pandoc -f docx --extract-media=./ -t markdown 'Towards DPLs.docx' -o dpls.md

3. used the query in ChatGPT "convert the following markdown to acmart latex format using 10pt:" and pasted the .md file into ChatGPT and copied its output into a file "test3.tex"

4. $ pdflatex test3.tex

And, tada, I have a PDF that looks like a paper.  I'm going to check it and look it over carefully and edit it, but, this gets me off the ground easily...

aside: If you have Word or something that exports to .docx, then you can use the process above. I used Apple's Pages instead of Word, because that's all I've got. (I guess I coulda used google docs?)

aside: I discovered a tool called "mammoth" that converts .docx to .html.  I was going to try that next, but, it looks like I don't need to bother.
aside: I needed to install pandoc and mactex on my Mac. Both seem to be available to linux.

aside: the --extract-media incantation saves the .pngs into a subdirectory and lets pdflatex find them, so I didn't have to futz with markdown's deficiencies, I just copy/pasted screenshots into the WYSIWYG editor and let the machine do the work for me.
