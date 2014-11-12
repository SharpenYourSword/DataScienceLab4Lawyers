# Data Scrubbing

```bash
# create a directory for work cd into it
mkdir datalab
cd datalab

# Download, or "wget" consumer finance complaint database
wget --no-check-certificate https://data.consumerfinance.gov/api/views/x94z-ydhh/rows.csv?accessType=DOWNLOAD

# rename complaints.csv and view first 10 rows
mv rows.csv\?accessType\=DOWNLOAD complaints.csv

# explore the file
head complaints.csv
head -n 20 complaints.csv
tail complaints.csv
wc -l complaints.csv

# complaints submitted via Web
grep Web complaints.csv | wc -l


# use grep and wc to quickly and roughly count complaints by year
grep "/2014" complaints.csv | wc -l
grep "/2013" complaints.csv | wc -l
grep "/2012" complaints.csv | wc -l
grep "/2011" complaints.csv | wc -l
grep "/2010" complaints.csv | wc -l

# use a slightly more precise pattern to match first dates
grep "/2010" complaints.csv | wc -l
```

```bash
# what products?
awk -F "," '{ print $2 }' complaints.csv 

# direct to file
awk -F "," '{ print $2 }' complaints.csv > productlist

# explore summary file of products
wc -l productlist
sort productlist | uniq -c
awk -F "," '{ print $2 }' complaints.csv | sort | uniq -c 
awk -F "," '{ print $2 }' complaints.csv | sort | uniq -c | sort -n
```

```bash
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



## Scrubbing the complaints data

We have a problem, there are commas within quotes. This will mess up our ability to split the file into fields by commas.
To fix, we need to replace the `,` delimiter with `:` delimiter. (This involves replacing the commas in quotes, replacing all the delimiter commas and finally putting back the commoas in quotes.)

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
- we got commas inside of fields!

create script to clean up
- 

awk 'NR%2-1{gsub(/,/,"|")}1' RS=\" ORS=\" a.csv | sed 's/,/:/g' | awk 'NR%2-1{gsub(/\|/,",")}1' RS=\" ORS=\"
awk 'NR%2-1{gsub(/,/,"|")}1' RS=\" ORS=\" complaints.csv | sed 's/,/:/g' | awk 'NR%2-1{gsub(/\|/,",")}1' RS=\" ORS=\" > complaints2.csv
(via http://www.unix.com/shell-programming-and-scripting/193311-help-awk-sed-need-replace-commas-between-double-quotes-csv-file.html)
awk -F ":" '{ print $6 }' c.csv 

awk -F ":" '{ print $2","$10 }' complaintscolon.csv 


time awk -F ":" '{ print $6 }' complaintscolon.csv | sort | uniq -c | sort -n 

time awk -F ":" '{ print $6 }' complaintscolon.csv | sort | uniq -c | sort -n > statetotals.csv
awk '{s+=$1} END {print s}' statetotals.csv 
310936


time awk -F ":" '{ print $12 }' complaintscolon.csv | sort | uniq -c | sort -n > statetotals.csv


password is ironlawyer


http://www.datasciencetoolkit.org/developerdocs
http://overapi.com/linux/
