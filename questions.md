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
* * * * * /home/aashish/hungry.sh 
#will press CTRL+O in crontab to save whatever name we wanna give or leave it as it is and press enter and will press CTRL+X to exit
#* means every minute , every hour , every day of month , every month , every day of the week this hungry.sh sript will run.


