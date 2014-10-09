---
layout:	post
title:	"csv Module in Python"
date:	2014-10-08 22:34
categories:	Python
---

CSV (Comma Separated Values) format is the most common import and export format for spreadsheets and databases which is widely used in financial industry or other data driven field. 

| Sort Order | Common Name | Formal Name                             | Type              |
|------------|-------------|-----------------------------------------|-------------------|
| 1          | Afghanistan | Islamic State of Afghanistan            | Independent State |
| 2          | Albania     | Republic of Albania                     | Independent State |
| 3          | Algeria     | People's Democratic Republic of Algeria | Independent State |

For example, above table can be represented as a sequence as follow:

	Sort Order,Common Name,Formal Name,Type  
	1,Afghanistan,Islamic State of Afghanistan,Independent State,  
	2,Albania,Republic of Albania,Independent State,  
	3,Algeria,People's Democratic Republic of Algeria,Independent State,

As a common tool for in same field, Python has a well support for CSV file, and it provides a module for efficiently handling them.

csv Module
----
csv module provides reader and writer objects for controlling read and write sequences. In this post, we will briefly introduce some useful functions to help reader get the idea about how to manipulate CSV format in Python

### Reading a CSV File
{% highlight python %}

	csv.reader(csvfile, dialect='excel', **fmtparams)

{% endhighlight %}

This function returns a reader object which will iterate over lines in the given csvfile. Following code shows us how to print out the table in previous section.

{% highlight python %}

	import csv
	with open('data.csv', newline='') as csvfile:
		data_reader = csv.reader(csvfile, delimiter=',')
		for row in data_reader:
			print(row)

{% endhighlight %}

We will have each row within an array with iteams sperated by commas.

{% highlight python %}

['Sort Order', 'Common Name', 'Formal Name', 'Type']
['1', 'Afghanistan', 'Islamic State of Afghanistan', 'Independent State', '']
['2', 'Albania', 'Republic of Albania', 'Independent State', '']
['3', 'Algeria', "People's Democratic Republic of Algeria", 'Independent State', '']

{% endhighlight %}

### Writing a CSV File
{% highlight python %}

	csv.writer(csvfile, dialect='excel', **fmtparams)

{% endhighlight %}

This function returns a writer object responsible for converting the user’s data into delimited strings on the given file-like object. Following code shows us how to store above arrays back to a CSV file.

{% highlight python %}

	import csv
	with open('data-out.csv', 'wb') as csvfile:
		data_writer = csv.writer(csvfile, delimiter=',')
		for row in data: # each row is an array
			data_writer.writerow(row)

		# or
		data_writer.writerows(data)

{% endhighlight %}

	# data-out.csv
	Sort Order,Common Name,Formal Name,Type
	1,Afghanistan,Islamic State of Afghanistan,Independent State,
	2,Albania,Republic of Albania,Independent State,
	3,Algeria,People's Democratic Republic of Algeria,Independent State,

### What do you think?
With the rapid development of NoSQL database, how will you compare CSV format with JSON?

Reference: [Python 3.4.2 Documentation](https://docs.python.org/3.4/library/csv.html)