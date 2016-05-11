---
layout: post
title: "Experiment - Bad Equity"
date: 2016-05-11 09:02
tags: [soundbashing, ocr, newspapers]
categories:
- Experiment
...

* Table of Contents
{:toc}

## Source Materials
The Shawville [Equity](http://theequity.ca/) is a weekly newspaper published in Shawville Quebec. It has published continuously since 1883, when it was first published in the county seat, Bryson. Recently, the Provincial Archives of Quebec ('[Bibliotheque et Archives Nationales du Quebec](http://collections.banq.qc.ca/)') scanned and OCR'd the [run from 1883 to 2010](http://collections.banq.qc.ca:8008/jrn03/equity/src/), using the materials held at the Equity's office, as part of a larger project to scan the journals of Quebec's long-established English communities.

I initially thought I would have to download all of the pdfs and extract the text layer from those, but in the repo, both the pdf and the txt file are available as separate files. I've re-posted an example [text file here](https://gist.github.com/shawngraham/8323899898cf016d5829f68394e63699).

I wondered: how good is the OCR? And, without manually checking each text file, can I auto-magically generate some sort of proxy for assessing this?

## Step 1. Obtaining the text files
Obtaining the text files was just a matter of correctly formatting a `wget` command. For whatever reason, I had a *lot* of trouble doing this. All I really needed to do was point wget at this directory:

[http://collections.banq.qc.ca:8008/jrn03/equity/src/](http://collections.banq.qc.ca:8008/jrn03/equity/src/)

like so:

`wget http://collections.banq.qc.ca:8008/jrn03/equity/src/ -A .txt -r --no-parent -nd –w 2 --limit-rate=10k`

but, for whatever reason, I felt I needed to generate a list of urls first, and *then* point wget at it. My `urlgenerator.py` was derived from the Programming Historian lesson on [applied archival downloading](http://programminghistorian.org/lessons/applied-archival-downloading-with-wget):

```python
urls = '';
f=open('urls.txt','w')
for x in range(1883, 2011):
    urls = 'http://collections.banq.qc.ca:8008/jrn03/equity/src/%d/\n' % (x)
    f.write(urls)
f.close
```

Ben also suggested a way of doing this in Ruby, to get right down to the month & day subdirectories:

```Ruby
t=Time.new(1883,05,01)
400.times { print"http://collections.banq.qc.ca:8008/jrn03/equity/src/#{t.year}/#{t.month}/#{t.day}/83471_#{t.year}-#{t.month}-#{t.day}.pdf\n"; t += 6*24*60*60 }
```
...although because the archives uses leading zeros for months 1 - 9 and days 1 - 9, some more fiddling is required. In the end, if I could've just sussed wget properly in the first place... ah well. Learning Ruby is clearly something I need to do.

- I downloaded every edition from 1883 through to the end of 1914, 1595 files. This took the better part of a day.

## Step 2. Has anyone else tried to do this?

And the answer is, yes, yes they have. A quick question on Twitter brought me to this post by [Ryan Baumann, Assessing OCR Quality](https://ryanfb.github.io/etc/2015/03/16/automatic_evaluation_of_ocr_quality.html). Later, I also had an excellent discussion with Ben Brumfield who pointed me to his work on [detecting handwriting in OCR'd texts](http://manuscripttranscription.blogspot.ca/2013/02/detecting-handwriting-in-ocr-text.html) and [code for the same](https://github.com/idigbio-aocr/HandwritingDetection/blob/master/code/find_labels_with_handwriting.rb). I haven't tried Ben's script yet. Below, I discuss trying to get Ryan's approach to work

## Step 3. Ryan's scripts
Ryan's scripts work by automatically detecting the language of each line in the ocr'd text. It uses a python module called `[langid](https://github.com/saffsd/langid.py)` to determine the probability that a text is in a particular language. Badly OCR'd lines make determining this difficult. His two scripts ([scorelines.sh](https://gist.github.com/ryanfb/0ee1082a597e200ca8c3#file-scorelines-sh) and [ocrquality.rb](https://gist.github.com/ryanfb/c9bd9a1ce0f6f7cb2a45#file-ocrquality-rb)) eventually should result in a value between 0 and 1 where 0 indicates no problem in assessing the language, hence, good OCR. (See Ryan's [tweet](https://twitter.com/ryanfb/status/730085822817566721)).

- first hiccup: `chmod`. Forgot I had to `sudo chmod 700 scorelines.sh` etc so that they'd work.
- second hiccup: depending on the txt file, the scripts would work, or crash spectacularly with a wide variety of errors. Because of that variety, my suspicion is that special characters in the text file - or possibly (probably?) weird encoding - is causing the scripts to break. A long trawl of stackexchange had me try `LANG=C` pre-pended, eg,

`$ LANG=C ./scorelines.sh filename.txt | ./ocrquality.rb`

and again, sometimes it worked, sometimes it didn't. If I ran `scorelines.sh` on its own, piping the output to file, which I then fed into `ocrquality.rb`, sometimes that would work when the two commands piped together wouldn't. And sometimes not. The only common denominator was the txt file itself.

> In which case, could the count of special characters be taken as a proxy for bad OCR?

- it's at this point that I should return to Ben's script, which parses each file with regex to count the myriad ways OCR can break, and creates a kind of tabular record of the same. For his purposes - identifying handwriting in printed text - this gives him an indication of which files to peruse more carefully. In a twitter exchange, we talked about 'why special characters?'. I showed him the sample txt (linked above) and he noted that I had way more special characters than him. This got me to thinking: what about Ryan Cordell's post on '[Qijtb the Raven](http://ryancordell.org/research/qijtb-the-raven/)?'. He uses [exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/) to see the metadata in the pdfs, which gives him crucial information on how the pdfs were generated. **I need to do this too**.
- At any rate, at this point, I wondered two things: 1) how carefully did they set up their OCR? and 2) is this related to the (likely?) possibility that the person running the OCR application does not speak English as a first language? Is there a quality control issue at play during the process of scanning?

## Step 4. Counting Special characters
- a script to count special characters was actually hard to find. I tried `wc` at first, to see if that could give me any useful output:

`find . -name '*.txt' | xargs wc`

...which, when piped to file, would give me the number of lines, number of words, and number of bytes. This output did not seem meaningful.
- more perusal of stackexchange found this:

```python
for f in *.txt; do
python -c "import collections, pprint; pprint.pprint(dict(collections.Counter(open('$f', 'r').read())))"
done
```
- this gave me the count for *every* character. This was a bit more useful, in that there is a fixed universe of possible characters, right? So I could maybe look at the ratio of the alphabet characters a-z to all the special characters. Since English doesn't use diacritical marks (but this being a paper in Quebec, there will be a certain amount of French marks), special characters, plus umlauts, etc, could be useful. **I have not yet calculated a ratio score**. I only just thought of it.
- on DH Slack, I described what I was up to in the 'DHAnswers' channel. Finlay McCourt re-wrote the script:

```python
#!/usr/bin/env python
import collections, pprint, re, sys
with open(sys.argv[1],'r') as file_in:
    chars = re.sub('[\s\w!!"#$%&()*+,-./:;<=>?@^_`{|}~\[\]\'\\\]','', file_in.read())
    counts = collections.Counter(chars)
pprint.pprint(counts.most_common())
```
...which counts the special characters, and puts them into a json-ish format. I called this script `bettercount.py` and put a bash wrapper around it: `for f in *; do python bettercount.py $f; done`. Thus, in my directory with the txt files, I piped commands together:

`./feedfile.sh > output.csv`

...which passes each file to bettercount.py. I opened `output.csv` in Sublime Text (which handles find & replace much better than Atom). I delete new lines to get each file and the number and count of special characters, one per line. I know I could have done this in my `bettercount.py` script, but *shrug*.

- I'm working on a Mac, and I'll be damned if I can figure out Numbers for working with spreadsheets. I copied my output to a [google spreadsheet](https://docs.google.com/spreadsheets/d/1g04mSEYUA11uGnW6QDOyOXOcrYh6DRlLOIvytXHTXd8/edit?usp=sharing). I added up the number of special characters. **Again, I could calculate a ratio here of numbers of special characters to possible special character types, to normalize things**. That might be a good idea.

## Step 5: 'Visualizing' the results: How bad is my OCR?
- I'm not keen on graphs at the moment. As part of a larger project, I'm trying to make visualization strange again so that the kinds of unconsicous bias that come from received notions of how-to-graph-things don't get in the way.
- So I sonified all this with Musicalgorithms.com, [version 3](http://musicalgorithms.org/3.0/index.html).
  - take the column of numbers to sonify. Remove line breaks so that all the numbers are on a single line, separated by a single space
  - paste this line into the musicalgorithms csv format:

```csv
# Of Voices, Text Area Name, Text Area Data
1,morphBox,
,areaPitch1,1140 2 991 [etc]
```
  - hit the 'load' button on Musicalgorithms, **paste** the formatted data into the box. (I say 'paste' because loading the csv directly, when you have this many 'notes', seems to introduce errors that bork the sonification).
  - I moved directly to 'play/download' and accepted all of the default parameter mappings.
  - I placed the resulting .mid file into Garageband to try to make the 'sonification' into rather more pleasing music. Well, 'pleasing' for a given value of pleasure, I guess.

## Result
- the 'music' can be heard at [soundcloud](https://soundcloud.com/shawn-graham-60451318/bad-equity)
- the defaults at musicalgorithms take the first few notes and apply a kind of _ritardo_ to slow them down, to make a kind of intro.
- I added the drum beat because part of my larger project is to acknowledge the performative, _capta_ aspect of all visualization. It's jarring, and that's deliberate, because I want the listener to reflect on the performative aspects of all visualizations... that's a post/paper for another day.
- You can hear the deep plunks when there are gaps in the record; you can hear the really high notes when a txt file is filled with garbage. The rather narrow range of notes implies that there are certain kinds of special characters that repeat over and over, which is suggestive of the kinds of errors that the OCR is making.
- Garageband makes a kind of visualization of the music, a player-piano roll-esque side-scroller, showing the values mapped over the 88 tones of the keyboard. This visualization, notwithstanding what I said above, is actually rather interesting:

![garagebandviz](https://pbs.twimg.com/media/CiI9f_oWsAEzwoN.jpg)

Note how the notes are rather dispersed in the earliest scans (at left, 1883) and become more and more tightly focussed as time spans towards 1914 (at right). That up-and-down tick at the right? My suspicion, yet to be confirmed, is that that corresponds to either a) new printing technology b) new typeface c) the move to Shawville when Shawville began to eclipse Bryson for prominence d) all of the above?

## What have I learned?
- dipping into the txt files from 1914, the eye can immediately determine that we have better quality scans. Using the special characters as a proxy for bad OCR **seems** to be valid. But how can I validate this impression?
- the patterning of the cloud of special characters **might** be giving me a way of exploring something of the materiality of printing? It reminds me of Ingrid's DH MA thesis at Carleton, where she adduced how small errors in reprints of _A History of the Pyrates_ said more about the culture/physical situation of printers than the world of authors
- For all my sonification, it's the visual player-piano roll that seems to be giving me the most useful information
- That said, the sound itself forces a different kind of attention whilst listening, and the narrowing of tone over time does come across. Or am I just looking for that, now that I've seen the player-piano roll? Another 'auditory hallucination'? see my [Programming Historian tutorial (under-review version)](http://programminghistorian.github.io/ph-submissions/lessons/sonification):

>What’s going on here? If that song was already known to you, you probably heard the actual ‘words’. Yet, no words are present in the song - if the song was not already familiar to you, it sounded like garbled nonsense (see more examples on Andy Baio’s website). This effect is sometimes called an ‘auditory hallucination’. This example shows how in any representation of data we can hear/see what is not, strictly speaking, there. We fill the holes with our own expectations. <br> Consider the implications for history. If we sonify our data, and begin to hear patterns in the sound, or odd outliers, our cultural expectations about how music works (our memories of similar snippets of music, heard in particular contexts) are going to colour our interpretation. This I would argue is true about all representations of the past, but sonifying is just odd enough to our regular methods that this self-awareness will help us identify or communicate the critical patterns in the (data of the) past.

## To do next:
- get more txt files
- re-run the analysis. Do the patterns hold up?
- try calculating ratios
- what are the special characters doing?
- use exiftool to consider the metadata
- how can I make this data haptic?
