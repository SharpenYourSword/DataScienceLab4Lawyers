# Session Outline

This is a rough outline of the hands-on lab session.

## You Can Do This
- green note, green note, gray note
- example legal terms
- example citation
- have you registered for an online service?
- who speaks a foreign language?
- who written paper 20 page pages or longer?
- who has gotten into law school?
- You are about to learn two dozen jargon terms, a new citation syntax, a couple of apps designed for lazy people. You can do this.
- Why learn this: point and click does not scale, sharing manual steps is error prone.

You need:
See the checklist.md file:
- terminal supporting unix commands
- bbedit or other text editor
- browser
- cheat sheet

## Love Your Terminal
- finding and launching the Terminal
- Simon says game
>	Stand up, we are going to play simon says
>	head, shoulders, 
>	simon says, who are you?
You are simon, your computer responds, like talking to siri, you don't even need to say "simon says"

- test driving: whoami, ls, ls -l, ls /, ls  pwd, cd
- two files in your root directory
- close terminal, open terminal and find size of the file /etc/passwd
- ls files and open in finder, too
	
- tab autocomplete 
	
- files: head, tail, head/tail -n, wc -l, cat

```bash
#useful files
head /usr/share/dict/words
head /usr/share/misc/flowers
```

- pipe: cat | more, cat | less
- try: number of files on your Desktop
	
- arrow up / arrow down
- move to home directory cd ~
- mkdir, rmdir
- mkdir, cd, nano

```bash
- cd ~/
- mkdir ironlawyer
- cp /usr/share/misc/flowers ./flowers
```

```
- grep Rose flowers
- clear
- grep love flowers
```

## Get Some Data
wget consumer finance complaint database (csv) 

```bash
wget http://freeengineer.org/learnUNIXin10minutes.html
more learnUNIXin10minutes.html

# get complaint data
wget --no-check-certificate https://data.consumerfinance.gov/api/views/x94z-ydhh/rows.csv?accessType=DOWNLOAD
ls
mv rows.csv\?accessType\=DOWNLOAD complaints.csv

# use head, tail, wc -l, cat and then ctl+c

# grep by year
grep "/2014" complaints.csv | wc -l
  129356
```

- jump over to snippets.md


## Repeat, at speed...
At speed, this pretty fast. Often faster than loading data into something.

- close terminal
- open terminal
- pwd
- mkdir ironlawyer2
- cd ironlawyer2
- get the file

```
# retrieve our file
wget --no-check-certificate https://data.consumerfinance.gov/api/views/x94z-ydhh/rows.csv?accessType=DOWNLOAD

# list to check for file
ls

# rename file
mv rows.csv\?accessType\=DOWNLOAD complaints.csv 

# study file
head complaints.csv 
wc -l complaints.csv 

# complaints submitted via Web
grep Web complaints.csv | wc -l

# count categories in file
awk -F "," '{ print $2 }' complaints.csv | sort | uniq -c | sort -n
   1 Product
1529 Money transfers
1557 Payday loan
9307 Consumer loan
9374 Student loan
37870 Bank account or service
40759 Credit reporting
41359 Credit card
43902 Debt collection
125276 Mortgage
```

## Break

## Everything is Virtual

- start a remote server
- ssh remote server
> Note: First login takes a long time

About the AMI (Amazon Machine Image) we are using
AMI | ami-fa169c92
name | DSTK-IronLawyer
OS | Linux
instance type | any, from micro to very large
username | ubuntu
password | ironlawyer
preloaded data | ~/ubuntu/4ironlawyer
based on | http://www.datasciencetoolkit.org/developerdocs#setup

see commandline-cheatsheet.md on how to login

## Own That Data File (CFPB Complaint Data)
- get that data file (see snippets.md)

## Scrubbing the data

We have a problem, there are commas within quotes!

```bash
awk -F "," '{ print $2","$10 }' complaints.csv 
...
1030034,Credit card,09/16/2014
1030010,Credit reporting,10/06/2014
1030004,Consumer loan,10/21/2014
1032050,Mortgage,Web
1032054,Debt collection,Web
1032077,Mortgage,Web
1032053,Student loan,09/16/2014
1032066,Debt collection,09/17/2014
...
grep 1032050 complaints.csv 
1032050,Mortgage,Conventional fixed mortgage,"Loan modification,collection,foreclosure",,NC,27597,Web,09/16/2014,09/16/2014,"Shellpoint Partners, LLC",Closed with explanation,Yes,
ctl+c
```

- we got commas inside of fields!

Create script to clean up (aka, search the web for help!)
```bash
awk 'NR%2-1{gsub(/,/,"|")}1' RS=\" ORS=\" a.csv | sed 's/,/:/g' | awk 'NR%2-1{gsub(/\|/,",")}1' RS=\" ORS=\"
awk 'NR%2-1{gsub(/,/,"|")}1' RS=\" ORS=\" complaints.csv | sed 's/,/:/g' | awk 'NR%2-1{gsub(/\|/,",")}1' RS=\" ORS=\" > complaints2.csv
(via http://www.unix.com/shell-programming-and-scripting/193311-help-awk-sed-need-replace-commas-between-double-quotes-csv-file.html)
awk -F ":" '{ print $6 }' c.csv 

awk -F ":" '{ print $2","$10 }' complaintscolon.csv 
```

- back to snippets.md
