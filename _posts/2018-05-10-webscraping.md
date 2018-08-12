---
layout: post
title: Webscraping with Wgetbigimg: /img/Netzwerk.jpg---
I had some huge problems with this one, because the links to download the wget-programme didn't work at my computer. 

finally, I found a link which worked. Here are the directions:


Publish a step-by-step explanation of what you have done as a blogpost on your website.

right klick on the webpage with all the links. - click on 'show codesource'
take a good look at the codesource
open the links of the article in the .xml-version.
We nned to figure out a regular expression to filter out all the links from the code.
I found this one:  href="text?doc=Perseus%3atext%3a2006.05.0009
I copied the code from the overview-website in a .txt-file
Then, I opened the 'find'-window (strg+f) and entered ** href="text(.*)" ** as a regular expression.
I copied the findings in a new .txt file.
Then, I wnated to clean the code.
In the search-window, I clicked on 'replace', and replaced **<a href="** and **" class="aResultsHeader"** with nothing.

Now I replaced ** text? ** with the beginning of the link code from the .xml-version of the links: **www.perseus.tufts.edu/hopper/dltext?**

Now I have the links and can start the webscraping-process as described on the website of our course.

Open powershell - cd to the folder where I put my file. 
write:
wget -i file_with_links.txt
wget -i links.txt -P -nc ./subfolder/