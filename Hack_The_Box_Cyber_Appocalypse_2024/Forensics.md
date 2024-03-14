Scenario : It Has Begun
![[fore_it_has_begun.png]]

After extracting the zip file we do get a script.sh file we can use cat to display the content of the file when going through the file content we see some string that looked reversed.
```
cat script
```
![[It_has_begun1.png]]
Further down in the file we found some interesting character that look like base64
![[It_has_begun2.png]]
lets use the rev command to get the content that was reverse
```
echo "user@tS_u0y_ll1w{BTH" | rev

```
![[It_has_begun3 3.png]]

lets decode the other part to get the rest of the flag using base64
```
echo "NG5kX3kwdVJfR3IwdU5kISF9" | base64 -d

```
![[It_has_begun4.png]]


Scenario: Urgent
![[urgent.png]]
After extracting the zip file we found .eml file. We can analyze the email using emlAnalyzer tool to analyze the eml file and do see that the file has an attachment which looks intresting.
```
emlAnalyzer -i Urgent\ Faction\ Recruitment\ Opportunity\ -\ Join\ Forces\ Against\ KORP™\ Tyranny.eml --extract-all --header --html 

```
![[urgent1.png]]
Displaying the content of the attached file It looks like the file content has been encoded with html.
```
cat onlineform.html
```
![[urgent2.png]]
Decoding html encoded content using python (usrlib.parse module)
![[urgent3.png]]
```
# A python script to decode html encoded text

import urllib.parse

url = '%3c%68%74%6d%6c%3e%0d%0a%3c%68%65%61%64%3e%0d%0a%3c%74%69%74%6c%65%3e%20%3e%5f%20%3c%2f%74%69%74%6c%65%3e%0d%0a%3c%63%65%6e%74%65%72%3e%3c%68%31%3e%34%30%34%20%4e%6f%74%20%46%6f%75%6>
html = urllib.parse.unquote(url)
print(html)

```
Running the script and Decoding the html encode content we can see our flag in the decode content.
![[urgent4.png]]

