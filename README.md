# CleanXml
Given a set of xml files with certain constraints, create new xml files containing only unique records

Due to some rather ridiculous restraints at work, I had a situation where I was receiving upwards of 150 xml files a day, and uploading them manually through a web front end. I quickly discovered that the records in the files sometimes contained duplicates, but the destination database was not supposed to contain duplicates. The team producing the xml files said they couldn't do anything about it, so I created this script to clean incoming xml files based on a canonical file of all records to date.

Essentially I'm duplicating the target database in xml form, but since the source team won't make the required changes and I have no permissions in either the source or destination systems, it is what it is.

This is also my first ever project in Python. Time from inception to the first full commit was 3 hours, including setting up PyCharm and reading the docs.
