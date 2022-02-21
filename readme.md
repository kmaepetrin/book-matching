# ISBN-Match

This is a tiny Jupyter notebook-based script for pulling ISBNs based on book data using the isbntools command line library. The goal is to produce a file that contains Goodreads-friendly upload file, which requires ISBN, so you can import old author/title-only reading trackers.

Think of this as a helper tool, not as a complete app. It makes a few steps very easy but still requires manual input.

### The notebook:
* Reads books by author and title from CSV
* Pulls ISBN using author and title lookup on isbntools
* Saves ISBNs in a pandas dataframe
* Exports the dataframe as csv
* Checks the matches against the ISBN log
* Produces text for manually validating matches

isbntools seems to be maybe ~80% accurate if you read a lot of comics or self-published ebooks, and closer to 95% accurate if you exclusively read traditionally published novels.

You will need to do some manual edits to make your file goodreads friendly. Check goodreads for their preferred CSV structure. (This notebook assumes you have mimicked their file format and titles; if you do not, you'll have to change the Pandas column titles in your .ipynb). 

After your export is done:
* Remove the brackets and apostrophes around the ['ISBN'] output. (You can just CTRL+F for [' and '] then replace with empty string in your csv editor of choice).
* Check match.txt file in plain-text to see whether the reverse ISBN lookup yields expected results. Manually update any ISBNs that did not match correctly.

### A few warnings:
isbntools struggles with a few publication types as a result of the fuzzy matching. You'll have to do some manual checking if you want to validate the results.

Keep an eye out for whether it correctly matched:
* Books that have ASINs (ie ebook-only self-published editions)
* Self-published or independently published books in general - even if they have ISBNs
* Single-issue comics, trade paperbacks, and especially comics that have published both
* Magazines (do not usually have ISBNs)
* Books with non-dictionary compound words in the title, or titles in other languages
* Short stories (some do have ISBNs, but many do not)
* Older ISBN10 codes that begin with the 0 character
* Books with multiple editions under different ISBNs
* Kickstarter-funded books (even if they have ISBNs)
* Poetry collections

### Requirements
* Jupyter Notebook or other .ipynb-capable environment
* Pandas
* [isbntools]('https://pypi.org/project/isbntools/')

The app has some limitations. isbntools seems to have approximately a ~1,000 lookup limit. I've built in a 2-second delay to each lookup, in order to attempt to mediate this. 

