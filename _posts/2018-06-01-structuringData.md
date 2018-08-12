---
layout: post

title: Structuring Data
subtitle: reformat dispatch and single out articles
bigimg: /img/Netzwerk.jpg
---



For this assignement as well I worked together with Erika, my colleague.
It was helpfull that we thought the code through in the course lesson.

Our task was to change the code from the last assignement properly.
That was the pseudocode I noted in the class:
Pseudocode:
0. Creating a variable for our data: creating a dictionary or better a list variable. List: 
1. create `TargetFolder`						same
2. collect the `list_of_files` from `SourceFolder`			same
3. loop through the `list_of_files`					same
    1. open each file (path: `SourceFolder`+`list_of_files`)		same
    2. find `issue_date`						same
    3. split the issue into `articles`					same
    4. create `counter`							same
    5. loop through `articles`						same
          1. update `counter` (+1)					same
	  2. extract info from data:
	        ##(itemID = "#ID: " + date+"_"+unitType+"_"+str(c)
                dateVar   = "#DATE: " + date
                unitType = "#TYPE: " + unitType
                header = "#HEADER: " + header
                text = "#TEXT: " + text) 
3. Var=“if)
4. Append to list
5. Text= „/n“ join (list)
6.saving

#exclude:
 #         2. remove XML tags
 #         3. do other cleaning, if necessary
 #         4. create `fileName` = `issue_date` + `_` + `counter`
 #         5. save text into a file: `TargetFolder` + `fileName`

I'll now show only the changings:
**0.: creating a list**
 
lof = os.listdir(source)

	for file in lof:
		if file.startswith("dltext"): #test if it is the right fileName	
			with open(source + "/" + file, "r", encoding="utf8") as newFile:
				text = newFile.read()

				# date
				date = re.search(r'<date value="([\d-]+)"', text).group(1)

				# splitting into articles/items
				split = re.split("<div3 ", text)

				c = 0 # article counter
				#loop through the split documents
				for s in split[1:]:
					c += 1
					s = "<div3 " + s # restore the integrity of items
				

					# find a unitType
					try:
						unitType = re.search(r'type="([^\"]+)"', s).group(1)
					except:
						unitType = "noType"
						print(s)

					# find a header
					try:
						header = re.search(r'<head>(.*)</head>', s).group(1)
						header = re.sub("<[^<]+>", "", header)
					except:
						header = "NO HEADER"
					
					#replace xml markup with blank spaces
					text = re.sub("<[^<]+>", "", s)
					text = re.sub(" +\n|\n +", "\n", text)
					text = re.sub("\n+", "", text)

					#generate itemID
					itemID = date+"_"+unitType+"_"+str(c)
		
					# creating a text variable
					textvar = "\t".join([itemID,date,unitType,header,text])+"\n"
				
					#append it to the list
					theList.append(textvar)

	# saving each line of the list to the new file (it only accepts strings)
	with open(target+"/"+"result"+".tsv", "w", encoding="utf8") as tsvFile:
		for line in theList:
			tsvFile.write(line)






