# SQL injection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2

![Screenshot 2024-05-07 093605](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/d18d89c9-58e3-4a87-bcb4-7cec0088ad69)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![Screenshot 2024-05-07 093638](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/457af7c5-b857-4207-8d61-845f8b203cc9)






Select Multidae from the menu listed as shown above. You will get the page as displayed below:


![Screenshot 2024-05-07 093657](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/a595294d-a933-4bba-a8e5-c2041311c779)

Click on the menu Login/Register and register for an account

![Screenshot 2024-05-07 094019](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/069ff42d-838b-47f5-b9be-6e71e19e25bb)



Click on the link “Please register here”

![Screenshot 2024-05-07 094036](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/4bb839f2-c4a3-42ab-95dc-95d8fb6084d8)




Click on “Create Account” to display the following page:

![Screenshot 2024-05-07 094101](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/15dc7c03-f7de-4c68-bf11-84f1d3cd43c5)


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/99360764-4aec-4418-818d-526f62a56a5d)


Click “Login”. The logged in page will show as below:

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/6bab1b4e-62df-4af2-b367-5449d122645b)



## Bypassing login field

*The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”
=================================================================*
If you face error in registration follow the following steps in metasploitable 2:



This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/bd1d19f2-3c56-435f-b682-9abbd37b8e2f)



Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/be0913be-97b7-4a22-98ec-0e5795d0574d)



Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/0de29235-82f7-48d6-9365-6ac040f520dd)

 Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/b258fff9-d8ce-4891-a197-2e949f453d6a)


Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/7fd0aca7-4d75-4d27-ae42-df93affc0a2c)


===============================================================

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password. 

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/66174de4-2c3e-4f5b-962a-fb5c0e3af1db)


Click the login button and you will see it enter into the administrator page.

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/ef98b40e-ef37-4d22-b743-cf9dad0a86b1)



## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/16faf4af-a57b-4a9c-a520-0151b5d9517f)
![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/1bf8ea0b-5345-4c13-9133-707c5b6a1552)
![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/a27e89f2-ac41-4ded-8122-4f487c5f0052)
![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/b7c38d3a-767a-44fc-98ea-1f0343f6302b)
![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/daa3d0f8-d1c0-4f6a-800a-4536e83d0e32)


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.


![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/a191c3f4-5f9b-4a0e-b2db-4c5fe1f0893a)






Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/200b9b2d-08bd-426d-ab98-766bfe59d7c4)



After adding the order by 6 into the existing url , the following error statement will be obtained:

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/6dbebec8-dfb1-4d4e-9c35-ffc6660963ff)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/ef87ffd9-02b9-48bd-a57c-e92924a383b8)


 As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/7bc6c6d6-ddea-464e-9718-99891e7f1a10)



Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/fcdcc679-9a35-4fb2-9337-a878f7f3f26a)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/e97e23ce-892b-45be-b534-40cb03cb7106)



Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/abinayasangeetha/sqlinjection/assets/119393675/8b1d65e5-aa47-498c-85a5-8701729430db)



The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’


http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details



The url once executed will  retrieve table names from the “owasp 10” database.
##Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.







The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details 



Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details



## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details



the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).





## RESULT:
The Social Engineering Toolkit (SET) is used to create backdoor is  examined successfully
