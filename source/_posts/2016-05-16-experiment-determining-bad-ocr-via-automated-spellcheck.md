---
layout: post
title: "Experiment - Determining Bad OCR via Automated Spellcheck"
date: 2016-05-16 13:10
tags: [soundbashing, ocr, newspapers]
categories:
- Experiments
...

* Table of Contents
{:toc}

# Misspelled words as indicator
In '[Bad Equity][94b590a3]', I ran an experiment trying to sonify the dirtiness of the OCR. It was suggested to me by Ben Brumfield (in DH Slack) that perhaps something like [Aspell](http://aspell.net/) might be a useful avenue to pursue.

  [94b590a3]: http://smgprojects.github.io/experiment-bad-equity/ "Experiment - Bad Equity"

The following script runs each text file in turn through Aspell's spell checker. The basic idea is to compare the number of 'mispelled' words (per Aspell's English Canadian dictionary) to the total number of words in each document. Thus, the closer that ratio gets to 1, the worse the OCR.

# The script

```sh
for f in *.txt; do
  totalbadwords="$(cat "$f" | aspell list -d en_CA --encoding utf-8 | wc -w)"
  totalwords="$(wc -w "$f")"
  echo "$totalbadwords, $totalwords" >> "finalscore.csv"
done
```

(also on [Github](https://gist.github.com/shawngraham/239edbcd7f5a495a7218bb93a9ce76a1))

The script iterates through each text file. `totalbadwords` is a variable for storing the result of each file being run through Aspell's dictionary, identifying 'mistakes', and then `wc` is used to count the number of these. `totalwords` just counts the number of words in each file. These values are echoed to a csv file so that I can open it in a spreadsheet or wherever to count, graph the result. Yes, I could do that in the script too I expect, but trying to write scripts that do one thing and one thing only.

# output

Currently, the output is sitting on my laptop, and [here on gdocs](https://docs.google.com/spreadsheets/d/1AfowhLwZQuuYMZtTDrD0riW33UPPxlgjwSumAJBrU2M/edit#gid=1997085128).

# graphs

I tweeted some of the resulting graphs. In reverse order:

[https://twitter.com/electricarchaeo/status/730781961506160642](https://twitter.com/electricarchaeo/status/730781961506160642)

[https://twitter.com/electricarchaeo/status/730571625540820993](https://twitter.com/electricarchaeo/status/730571625540820993)

[https://twitter.com/electricarchaeo/status/730571270870437889](https://twitter.com/electricarchaeo/status/730571270870437889)

![img](https://pbs.twimg.com/media/CiRCUkIW0AQTkQ-.jpg)

# interpretation

The consistent values in the .75 range are all editions where the Provincial Archives have inserted a placeholder for a missing edition.

![img](https://pbs.twimg.com/media/CiODBX-WUAItMhm.jpg)

Filter those out:

![img](/images/ocr-spell.png)
