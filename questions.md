## Task 1 
 
In this task you are asked to use the ls command to list out all of the contents in 
your /etc and your /run folders. 
First, deal with the /etc folder. Use the ls command to list it's contents and redirect those 
contents to a file called file1.txt  
Do the same for the /run folder but redirect the content to a file called file2.txt instead.

## Task 2 
 
Once you have file1.txt  and file2.txt  created, it is time to complete task 2 of the 
assignment! 
In Task 2, you are asked to use the cat command to combine together 
(i.e. concatenate) file1.txt  and file2.txt  into another file called unsorted.txt  
But, in the same pipeline you are also asked to also use the sort command with the r option 
to to reverse the output from the cat  command and redirect that reversed output to another file 
called reversed.txt  
Task 2 should all be completed in one pipeline.

## Task 3
 
In this task you are asked to create a folder called super_secret_stuff and inside that folder to 
place a file called top_secret.txt 
top_secret.txt may contain whatever content you wish. 
Once you have created the file, use the updatedb command and the locate command to find 
the path to top_secret.txt .  
Using redirection, save the path that the locate command gives you to a new file called 
secret_place.txt in your home directory.

## Task 4
 
## Part A) 
In this task, you are going to create an advanced pipeline that will create a sorted list of 
the various file sizes on your system. 
Firstly, use the find command to search your entire file tree; starting from the / 
directory, for all files that are over 1 MebiByte in size. Use the maxdepth option to limit 
the find command’s search to only go 4 levels deep. The search should only show 
files, not directories. 
Use the -exec  option of the find command to run the ls -lh command on each of 
those results. 

## Part B) 
Sort the output from Part A using the sort command. You should sort the data so that 
the largest file sizes are at the top of the list and the smallest file sizes are at the bottom.  
Using redirection, output this data to a file called filesizes.txt in your home directory. 

## Task 5
 
In this task you are asked to create a bash script called hungry.sh in your home directory. 
hungry.sh should do two things: 
Firstly, it should output the text I am hungry. Feed me data. to a file in your home directory 
called demands.txt  
Secondly, hungry.sh should also output the date and time that the demand was made to a file 
in your home directory called demands.log  
Do ensure that each output is appended to the previous one. 

## Task 6
 
Once you have created hungry.sh , you are tasked to edit your crontab  and add a new row 
so that hungry.sh runs every minute. Your computer loves data, after all

Labas ! so lets solve these above questions

Solution 1- 

ls /etc >> file1.txt
ls /run >> file2.txt

Solution 2-

cat file[1,2].txt | tee unsorted.txt | sort -r >> reversed.txt 
##You can also write- cat file1.txt file2.txt | tee unsorted.txt | tac >> reversed.txt 

Solution 3-

mkdir super_secret_stuff && touch ~/Desktop/super_secret_stuff/top_secret.txt
sudo updated
#Will enter the password
locate top_secret.txt
##&& i used a operand to save time and it means if first commands get executed then only execute 2nd one. Lmao am feeling pro hahaha

Solution 4-

PARTa-
          sudo find / -maxdepth 4 -type f -size +1M -exec ls -lh {} \;
#giving sudo so error permission deny dont comes
#\; ends the exec command


Partb-
          sudo find / -maxdepth 4 -type f -size +1M -exec ls -lh {} \; | sort -hrk 5 >> ~/filesizes.txt

Solution 5-

#!/bin/bash
echo "I am hungry. Feed me data." >> "$HOME/demands.txt"
date >> "$HOME/demands.log"

Solution 6-

crontab -e
***** /home/aashish/hungry.sh 
#will press CTRL+O in crontab to save whatever name we wanna give or leave it as it is and press enter and will press CTRL+X to exit
#* means every minute , every hour , every day of month , every month , every day of the week this hungry.sh sript will run.



## EXTRA QUESTIONS FOR SHELL SCRIPTING


## Task 7-The goal of this exercise is to create a shell script that adds users to the same Linux system as the 
script is executed on. 
Scenario: 
Imagine that you're working as a Linux System Administrator for a fast growing company.  The latest 
company initiative requires you to build and deploy dozens of servers.  You're falling behind 
schedule and are going to miss your deadline for these new server deployments because you are 
constantly being interrupted by the help desk calling you to create new Linux accounts for all the 
people in the company who have been recruited to test out the company's newest Linux-based 
application. 
In order to meet your deadline and keep your sanity, you decide to write a shell script that will create 
new user accounts.  Once you're done with the shell script you can put the help desk in charge of 
creating new accounts which will finally allow you to work uninterrupted and complete your server 
deployments on time. 
Shell Script Requirements: 
You think about what the shell script must do and how you would like it operate.  You come up with 
the following list. 
The script: 
● Is named "add-local-user.sh ". 
● Enforces that it be executed with superuser (root) privileges.  If the script is not executed with 
superuser privileges it will not attempt to create a user and returns an exit status of 1. 
● Prompts the person who executed the script to enter the username (login), the name for 
person who will be using the account, and the initial password for the account. 
● Creates a new user on the local system with the input provided by the user. 
● Informs the user if the account was not able to be created for some reason.  If the account is 
not created, the script is to return an exit status of 1. 
● Displays the username, password, and host where the account was created.  This way the 
help desk staff can copy the output of the script in order to easily deliver the information to 
the new account holder.


Answer-  

#!/bin/bash

#  Enforces that it be executed with superuser (root) privileges.
if [[ "${UID}" -ne 0 ]]; then

echo "Use sudo along with the command to run this script"

exit 1

fi

# Prompts the person who executed the script to enter the username (login), the name for
person who will be using the account, and the initial password for the account.


# lets solve this first by using read -p command ( use man command if u wanna know more bout the below command)

read -p "Please enter your username: " login

read -p "Please enter your name: " name

read -p "Please enter your password: " password

# Creates a new user on the local system with the input provided by the user.

useradd -c "${name}" -m "${login}"

# Informs the user if the account was not able to be created for some reason.

if [[ "$?" -ne 0 ]]; then

echo "In the name of God,please try again, you did something wrong and acc didnt got created"

exit 1
fi
# Displays the username, password, and host where the account was created

echo "${login}:${password}" | chpasswd

#set force password
passwd -e "${login}"

HOSTNAME=$(hostname)

echo "--------------------------------"

echo "User created successfully"

echo "Username : ${login}"

echo "Password : ${password}"

echo "Host     : ${HOSTNAME}"

echo "--------------------------------"

## TASK 8
 
The goal of this exercise is to create a shell script that adds users to the same Linux system as the 
script is executed on. 
Scenario: 
The help desk team has been using the "add-local-user.sh " script you created.  They're really 
happy that they don't have to wait on you to create new accounts. :-)  However, they would like for 
you to make a couple of changes to the script when you get a chance. 
They're tired of coming up with a unique password for each user they create.  As a matter of fact, 
Jim keeps using "password" as the password for every account.  They think it would be great if the 
script automatically generated a password for each new account.  That way Jim and the rest of the 
team won't have to even think about passwords any longer. 
Also, they think it would be a little more efficient if they could just specify the account name and 
account comments on the command line instead of being prompted for them.  They already know 
what they are going to type so they would just rather type it all in at one time. 
Since you're happy that you're not the one creating all the new accounts any longer, you decide to 
accommodate their requests.  (You're so nice!) 
Shell Script Requirements: 
You have your requirements from the "add-local-user.sh " script you created.  You decide to use 
those as the basis for your new requirements.  You come up with the following list. 
The script: 
● Is named "add-new-local-user.sh ".  (You add the word new to distinguish it from the 
original script.) 
● Enforces that it be executed with superuser (root) privileges.  If the script is not executed with 
superuser privileges it will not attempt to create a user and returns an exit status of 1. 
● Provides a usage statement much like you would find in a man page if the user does not 
supply an account name on the command line and returns an exit status of 1. 
● Uses the first argument provided on the command line as the username for the account.  Any 
remaining arguments on the command line will be treated as the comment for the account. 
● Automatically generates a password for the new account. 
● Informs the user if the account was not able to be created for some reason.  If the account is 
not created, the script is to return an exit status of 1. 
● Displays the username, password, and host where the account was created.  This way the 
help desk staff can copy the output of the script in order to easily deliver the information to 
the new account holder. 

## ANSWER

#!/bin/bash

#Tasks to complete in this script
#Making sure the script is being executed with superuser privileges
#Supplying username as an argument to the script
#Optionally we can provide a comment for the account as an argument
#A password should be automatically generated for the account


if [[ "${UID}" -ne 0 ]];then

echo "Execute the script with sudo command mate"

exit 1

fi

#If they don't supply at least one argument, then give them help

if [[ "${#}" -lt 1 ]];then

echo "Please supply atleast 1 argument by typing on the command line"

echo "Create an account on the local system"

exit 

fi

USER_NAME="${1}"

shift

COMMENT="${@}"

PASSWORD=$(date +%s%N | sha512sum | head -c48)

#Creating the user with the password

useradd -c "${COMMENT}" -m ${USER_NAME}

#If useradd command doesnot succeed, then will tell user something went wrong

if [[ "${?}" -ne 0 ]];then 

echo "The account could not be created"

exit 1 

fi

echo "${PASSWORD} |chpasswd"

if [[ "${?}" -ne 0 ]];then

echo "Password for the account could not be set"

exit 1

fi

passwd -e ${USER_NAME}

echo 

echo "username: "

echo "${USER_Name}"

echo 

echo "password: "

echo "${PASSWORD}"

echo

echo "host"

echo "${HOSTNAME}"

exit 0

## TASK 9 

Goal:
The goal of this exercise is to create a shell script that adds users to the same Linux system as the script is executed on.  Additionally this script will conform to Linux program standard conventions.

Scenario:
The help desk team loves the script you created for them.  However, they have just one more request.  They want the script to only display the details that they need to send to the user after they create their account.

You decide that's an easy enough change.  Because you know you'll have to use redirection to accomplish the task, you decide add redirection in other places in the script to make it conform to standard UNIX/Linux program conventions.  Namely, sending errors to STDERR.

Shell Script Requirements:
You have your requirements from the "add-new-local-user.sh" script you created.  You decide to use those as the basis for your new requirements.  You come up with the following list.

The script:

Is named "add-newer-local-user.sh".  (You change the name slightly to distinguish it from the previous script.  NOTE: In the real world you could have easily kept the same script name.  I just want to use a different name for the purpose of discussing specific scripts in the class.)

Enforces that it be executed with superuser (root) privileges.  If the script is not executed with superuser privileges it will not attempt to create a user and returns an exit status of 1.  All messages associated with this event will be displayed on standard error.

Provides a usage statement much like you would find in a man page if the user does not supply an account name on the command line and returns an exit status of 1.  All messages associated with this event will be displayed on standard error.

Uses the first argument provided on the command line as the username for the account.  Any remaining arguments on the command line will be treated as the comment for the account.

Automatically generates a password for the new account.

Informs the user if the account was not able to be created for some reason.  If the account is not created, the script is to return an exit status of 1.  All messages associated with this event will be displayed on standard error.

Displays the username, password, and host where the account was created.  This way the help desk staff can copy the output of the script in order to easily deliver the information to the new account holder.

Suppress the output from all other commands.

## ANSWER

#!/bin/bash

if [[ "${UID}" -ne 0 ]];then

echo "Please run with sudo or as root" >&2

exit 1

fi


if [[ "$#" -lt 1 ]];then

echo "Create an account on the local system with the name of USER_NAME and comments field of COMMENT" >&2

exit 1

fi

USER_NAME="${1}"

shift

COMMENT="${@}"

PASSWORD=$(date +%s%N | sha512sum | head -c48)

useradd -c "${COMMENT}" -m "${USER_NAME}" &> /dev/null


if [[ "${?}" -ne 0 ]];then

echo "Account could not be created" >&2

exit 1

fi

echo "${USER_NAME}:${PASSWORD}" | chpasswd &> /dev/null

if [[ "${?}" -ne 0 ]];then

echo "Password for the ${USER_NAME} could not be set" >&2

exit 1

fi

echo

echo "username:"

echo "${USER_NAME}"

echo

echo "password:"

echo "${PASSWORD}"

echo

echo "host:"

echo "${HOSTNAME}"

exit 0

