# Regular Expressions

In the following, you will parse information from text-based files with the command line and Unix tools and Python in the next step. Please note that even though the files are provided as structured csv files you are not supposed to simply read out the columns, but you should use regular expressions instead.

## Parsing contact information from the command line

In this directory, you will find a txt-file called `csv/contacts.csv`. Use regular expressions to extract the following information from it.

Remember that you can use different tools like `grep`, `awk`, or `sed` to use regular expressions from the command line. Pipes might also be helpful. 

You can add your command line in- and outputs directly to this README file. Alternatively, you can write a bash script with all commands and commit it to this directory.

### 1. Extract all email addresses from the text.

Input:
```
grep -oE '[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}' csv/contacts.csv
```
Output:
``` 
john.doe@example.com
jane.smith@gmail.com
mjohnson@yahoo.com
lharris@hotmail.com
rbrown@company.com
alice.white@domain.org
dgreen@domain.net
eblack@webmail.com
cblue@provider.com
ssilver@university.edu
``` 
### 2. Extract all phone numbers from the text.

Input:
```
grep -oE '\(?[0-9]{3}\)?[-. ]?[0-9]{3}[-. ][0-9]{4}' csv/contacts.csv
```
Output:
``` 
(555) 123-4567
(555) 987-6543
(555) 555-5555
(555) 321-6789
(555) 876-5432
(555) 432-5678
(555) 246-1357
(555) 531-2468
(555) 864-9753
(555) 975-8642
``` 
### 3. Extract all names that start with the letter ‘J’.

Input:
``` 
awk -F',' '$1 ~ /^J/ {print $1}' csv/contacts.csv
```
Output:
```
John Doe
Jane Smith
``` 
### 4. Extract all street names that contain the word 'St'.

Input:
```
grep -oE '\b[A-Za-z0-9 ]+St\b' csv/contacts.csv
```
Output:
``` 
123 Main St
456 Oak St
654 Cedar St
987 Elm St
246 Birch St
135 Walnut St
864 Chestnut St
``` 
### 5. Extract all addresses in ‘USA’.

Input:
```
awk -F',' '$4 ~ /USA/ {print $2 "," $3}' csv/contacts.csv
```
Output:
```
123 Main St, Anytown
456 Oak St, Sometown
789 Pine Rd, Othertown
321 Maple Dr, Newcity
654 Cedar St, Oldtown
987 Elm St, Smalltown
246 Birch St, Uptown
135 Walnut St, Middletown
864 Chestnut St, Metropolis
975 Cypress Ave, Bigcity
``` 
### 6. Extract the last names of all people.

Input:
```
awk -F',' '{print $1}' csv/contacts.csv | awk '{print $2}'
```
Output:
``` 
Doe
Smith
Johnson
Harris
Brown
White
Green
Black
Blue
Silver
``` 
### 7. Extract all email domains (part after the @ sign).
Input:
```
grep -oE '@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}' csv/contacts.csv | sed 's/@//'
```
Output:
```
example.com
gmail.com
yahoo.com
hotmail.com
company.com
domain.org
domain.net
webmail.com
provider.com
university.edu
``` 
### 8.	Extract all instances of the first name ‘David’ along with their full address (street and city).
Input:
```
awk -F',' '$1 ~ /^David/ {print $1 "," $2 "," $3 "," $4}' csv/contacts.csv
```
Output:
```
David Green, 246 Birch St, Uptown, USA
``` 
### 9.	Find all entries where the phone number ends with ‘7’.

Input:
``` 
awk -F',' '{if ($6 ~ /7[[:space:]]*$/) print $6}' csv/contacts.csv
```
Output:
```
 (555) 123-4567
 (555) 246-1357
``` 
### 10.	Extract all instances of first names that end with the letter 'e'.

Input:
``` 
awk -F',' '{split($1, name, " "); if (name[1] ~ /e$/) print name[1]}' csv/contacts.csv
```
Output:
```
Jane
Mike
Alice
``` 
## Parsing product orders with Python

In this directory, you will find another file called `csv/orders.csv` and also a short Python script that reads the file and parses all numbers with a regular expression. Please extend the script such that it also print the following extracted text pieces.

1.	Extract all order numbers from the text. 
2.	Extract all product names.
3.	Extract all prices.
4.	Extract all order dates.
5.	Find all orders for products priced over $500. (You are allowed to use Python to filter the list.)
6.	Change the date format to DD/MM/YYYY. (Note the re.sub() method)
7.	Extract product names that have more than 6 characters.
8.	Count the occurrence of each product in the text. (You may want to use the Counter class from the collections package.)
9.	Extract the orders with prices ending in .99.
10.	Find the cheapest product. (You may want to use Python's min() method.)
