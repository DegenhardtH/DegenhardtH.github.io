---

layout: post

title: Text Markup [TEI XML]
subtitle: Clean the Dispatch
bigimg: /img/Netzwerk.jpg
---



I had some problems with this Assignement as well and finally got help from my colleague Erika, without her and her boyfriends help I would have been unable to work it out.


To import the files from my folder, I used "import os"
then I positioned the path to the directory I wanted to take the files from.
>>input_path = os.path.relpath(".\\files")
>>output_path = os.path.relpath(".\\res")
As told from Erika, I used the command os.listdir to get the files.
>>input_filelist = os.listdir(".\\files")
>>output_filelist = os.listdir(".\\res")
Now, it was time to find some regular expressions. The regular expressions I used where: 
>>div3[^<]+article[^<]+>
To open and save the documents, wrote a for loop to store the files in each subfolder :

>>for fileName in input_filelist:
>>>with open(".\\files\\" + fileName, 'r', encoding="utf8") as file_in:
>>>>data = file_in.read()

	
>>>with open(".\\res\\" + newfile, 'w', encoding="utf8") as file_out:
>>>>file_out.write(text) 
(for the end of the for-loop)

to split the files in articles I defined a variable 'results' using the regular expressions I picked as 're.split("<div3[^<]+article[^<]+>", data)':
>> results = re.split("<div3[^<]+article[^<]+>", data)

I defined anoter Variable 'n' first as 0. Then I wrote another for loop to put new data in 'results'; 
there I defined a new Variable called 'newfile' as 'fileName + "_" + str(n) + ".xml"'; and added to the Variable 'n' n+1. 
That meant, that every new file which was extracted got a fileName and one number higher that the article beforehand.
at last, I also had to replace the xml markup to clean it: I defined a new Variable 'text' as 're.sub("<[^<]+>", "", dataNew)'
>> text = re.sub("<[^<]+>", "", dataNew)


That is the code:




	import re
	import os

	#define relative path
	input_path = os.path.relpath(".\\files")
	output_path = os.path.relpath(".\\res")

	input_filelist = os.listdir(".\\files")
	output_filelist = os.listdir(".\\res")

	#note to self: identify pattern(s) for articles
	#Pattern: <div3 type="article" n="4" org="uniform" sample="complete"> at the start of every article
	#regEx: <div3[^<]+article[^<]+>

	for fileName in input_filelist:
		with open(".\\files\\" + fileName, 'r', encoding="utf8") as file_in:
			data = file_in.read()
	
		#split files in articles
		results = re.split("<div3[^<]+article[^<]+>", data)
	
		#save each article with numerus currens
		n = 0
		for dataNew in results:
			newfile = fileName + "_" + str(n) + ".xml"
			#numerus currens
			n = n + 1
			#replace xml markup
			text = re.sub("<[^<]+>", "", dataNew)
		
		with open(".\\res\\" + newfile, 'w', encoding="utf8") as file_out:
			file_out.write(text)


	



´´´
