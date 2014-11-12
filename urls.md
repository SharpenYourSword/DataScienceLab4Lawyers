# Data URLs for Lab

## Consumer Finance Complaint Database
CFBP's database of complaints related to consumer financial products. Covers 2010 to 2014 as of this posting, 50MB.

What:                         | URL:
------------------------------|------
Consumer Finance Complaint Database | http://www.consumerfinance.gov/complaintdatabase/
CSV file of Consumer Finance Complaint Database | https://data.consumerfinance.gov/api/views/x94z-ydhh/rows.csv?accessType=DOWNLOAD
Online browsing | https://data.consumerfinance.gov/dataset/Consumer-Complaints/x94z-ydhh?

## IRS Statistics of Income (SOI) Data for 2012
IRS published aggregated stats on income organized by zip codes
Name:                         | URL:                                       
------------------------------|--------------------------------------------
IRS SOI 2012 data sets | http://www.irs.gov/uac/SOI-Tax-Stats-Individual-Income-Tax-Statistics-2012-ZIP-Code-Data-%28SOI%29
2012 csv file incl. AGI* | http://www.irs.gov/file_source/pub/irs-soi/12zpallagi.csv
IRS Tax Statistics Page | http://www.irs.gov/uac/Tax-Stats-2
> * Adjusted Gross Income


- http://www.consumerfinance.gov/hmda/#video
- http://www.ffiec.gov/hmda/hmdaproducts.htm
- http://www.ffiec.gov/hmda/hmdaflat.htm

http://www.ffiec.gov/hmdarawdata/LAR/National/2013HMDALAR%20-%20National.zip


## Reference URLs for Lab

Name:                         | URL:
------------------------------|--------------------------------------------
http://xkcd.com/1409/
http://aws.amazon.com/free/
http://www.datasciencetoolkit.org/developerdocs
http://overapi.com/linux/

# Window powershell tips
- Invoke-WebRequest http://rambletech.wordpress.com/ -OutFile c:\temp\blog.txt
- http://rambletech.wordpress.com/2011/09/21/windows-powershell-v3-includes-command-like-wgetcurl/
- grep in powershell http://dereknewton.com/2010/12/powershell-grep-equivalent/


# Command line for data science Reference
=========================================
- http://www.gregreda.com/2013/07/15/unix-commands-for-data-science/
`
	Let's assume our data, which we'll call data.csv, is pipe-delimited ( | ), and we want to sum the fourth column of the file.
	`cat data.csv | awk -F "|" '{ sum += $4 } END { printf "%.2f\n", sum }'
	
- http://jeroenjanssens.com/2013/09/19/seven-command-line-tools-for-data-science.html


# Cool Tools
=============
http://www.datasciencetoolkit.org
- https://datawrapper.de
- http://www.unixguide.net/unix/faq/1.3.shtml

