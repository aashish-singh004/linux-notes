#Linux Commands & bash scripting

#Before starting , just remember few small commands which will help you like CTRL+ALT+T will open your linux terminal then CTRL+L will clear the terminal, you dont
always need to write clear command in linux terminal which clears whatever is in the terminal, use these shortcuts , then if you wanna exit from terminal , do CTRL+D

##COMMANDS
echo --whatever u echo it will be pasted in teriminal 
example-- echo Hello --output will be Hello in terminal

cal --command wil tell you the current month and date too
example- cal --output will be current month and date too will be shown iin terminal , and if i use cal 2026 then entire year calender will be shown

date -- will tell u the date

cd -- changes directory goes to root level
cd ../.. -goes back to 2 level 
example if am in /home/user/projects/aashish and run cd ../..  , i will be in /home/user 
cd ..  goes back to one level

history -- this command will show all command history whatever we typed in terminal
history -c; history -w  just clear the history and write those changes in the terminal

which --it will just tell in which folder the command is 
example which echo  - output will be /usr/bin/echo 

man -- it helps us know more bout commands like if i wanna know what more command is there in cd and its use will do
man cd - it will open the manual page and then from it whatever command is userful, i will remember it and use to work fast in terminal
man -k cd --it will print us a conclusion of this command what is it , how its used etc in the terminal

mkdir creates folder fr us in the directory , mkdir -p creates folder under folder
touch creates files
cp - means copy something
mv - means move a file or folder whatever
rm - means delete but if u wanna delete a directory use 
rm -r  r here means recursive so it will recursivelly delete that directory/folder
rm -ri (foldername)  will delete that folder but because of i it will ask u first then delete like rm -ri ~/Backups/ it will delete Backups folder

| - means piping like take output of one command and give it as input to another 
example --  man -k which | less  it means whatever the result of that man -k command , use the less command on it

xargs - Some commands don’t accept input from pipe properly so xargs fixes that by converting input into arguments like
example-- ls *.txt | xargs rm so it will delete all the files ending with .txt and * is a wildcard will come into this now , just remembered haha

tee command save output to file AND show it on terminal screen too like
example- cat ~/Desktop/file.txt | tee Backup.txt
output will be - Heyy wsup on terminal screen as its the content of the file.txt and also one more file will be created as Backup.txt which will contain the 
same content as file.txt

#aliases are fr shortcut of a command like open text editor type whatever code u want and use in start alias then use ' in starting of the command and ending to'
then save it as .bash_aliases/or whatever name u want then if u want to run that code
example- i saved this in that .bash_alias --- alias bored='echo meowwww' Now whenever i type bored in terminal , meowww will be echoed , so tadada 
i made my own command

WILDCARDS like * star wildcard means anything, then so many are there which is helpful in day today task like ? matches exactly one character ??- matches 2 characters
[] matches any one character inside file like ls file[1-3].txt -ouput will be file1 file2 file3 as file1-file3 is already saved in my home directory
[!] matches everything except like ls file[!1].txt will show us all files except file1.txt


&& wildcard controls how command will run together like cp file1.txt && cd file1.txt if first command succeed then only 2nd command will run else nehh
|| or wildcard runs next command only if previous fails
; runs commands no matter what 

nano - can edit and create file using nano and can also write scripts using nano, will come to this later but lemme give example
nano hi.txt , then nano editor will be opened in terminal where i can type anything then press CTRL+O to save whatever name i want or just leave hi.txt
as it then i will do CTRL+X to exit , or if i want to write bash script using nano then will do
nano script.sh #!/bin/bash in the first line and continue #! is shebang and /bin is the path and bash is the interpreter.

sudo -  we run a command as a root aka admin
sudo su - we become a root user and gain all powers aka DORAEMON ; jokes apart lets continue

locate command is used for searching files using a pre-built database 
example locate *.txt will output everything ending with .txt 
locate -i *.TXT will give us same result as above command cause i means case in sensitive, if i want like only first 10 result. I can do
locate -i *.txt | head -n 3 output will be only 3 not full huge bundle of results
#locate command gives us from database so if database havent been updated like if i saved a file recently and then ask locate , no result will be there
#so better to use find command or if using locate for recent file do sudo su updatedb first then do locate

find - same as locate but find in real time 
example- find *.txt will locate everything ending with txt or more advance version if you wanna search specific like
find . -maxdepth 4 -iname "5.txt" -type f or if i wanna copy this or and send to ~/Desktop/copy_file folder use 
find . -iname "5.txt" -maxdepth 4 -type f -exec cp {} ~/Desktop/copy_file \;  exec means execute and {} means whatever the results is copy that
#if you replace exec with ok , then it will ask you before executing it but if files are big, it will be a headache

cat - this means concatenate , it read files and outputs on terminal, it can be piped too along with various commands to maximize its results and make task easy
tac command does same thing but in reverse order vertically and to do it horizontally words , use rev command
head command gets us what i need from file in rows like head -n 5 file.txt will get me first 5 words in vertical form
tail command is just same but it starts from last

sort command sorts data inside file , can sort folders too by piping sort command with ls or etc etc
sort -k sorts column in file , sort -r sorts in reverse order , sort -u removes duplicate texts
example sort -k 2 means sort column 2 in a file . sort -u means remove duplicate words in a file.

tar command is used to archieve files like
tar cvf archieve.tar ~/Desktop/Files/file[1-3].txt  .tar is a extension , c means create v here means verbose like show us the progess on terminal,
f means file name
#To unarchieve aka extract it use xvf archieve.tar , and to compress archieve it use
tar -czvf archive.tar.gz ~/Desktop/Files/file[1-3].txt   gz is also a extension, gotta have to use it , and to extract use
tar -xzvf archive.tar.gz and to view tar file use tar -tf archieve.tar it will look and output whatever is inside that tarball

##### Bash scripting notes (my understanding)

exit status -- every command in linux gives a result after running
0 means success
anything other than 0 means error

echo $?  -- this shows last command result

example:
ls file.txt
echo $?   # if file exist then 0 otherwise not 0


#### conditions

we can check result using if

if [ $? -eq 0 ]
then
  echo "command worked"
else
  echo "command failed"
fi

-eq means equal
-ne not equal
-gt greater than
-lt less than


#### functions

function is used to reuse code

example:

myfun() {
  echo "hello from function"
}

myfun

also we can return value

myfun() {
  return 1
}

myfun
echo $?   # will print 1


#### wildcards

used to match files

*  means anything
?  means single character
[] means range

example:

ls *.txt
ls file?.txt
ls file[1-3].txt


#### case statement

better than multiple if else

example:

case $1 in
  start)
    echo "starting"
    ;;
  stop)
    echo "stopping"
    ;;
  *)
    echo "unknown input"
    ;;
esac


#### logging

we can save output in file

echo "started script" >> log.txt

>  overwrite file
>> append file

2>  used for error

example:
ls wrongfile 2> error.txt


#### while loop

used to repeat

example:

i=1
while [ $i -le 5 ]
do
  echo $i
  ((i++))
done


#### debugging

bash -x script.sh  # show what is happening

set -x  # print commands
set -e  # stop if error


#### sed command

used to change text in file

example:

sed 's/old/new/' file.txt

this will replace first match

for all:
sed 's/old/new/g' file.txt


#### important things i understood

always check exit status when writing scripts
use echo to debug
write small scripts first
functions make code clean
logging helps when script fails

Till now i have learnt this only , from tomorrow onwards i.e 22nd of april , will learn from this video on
## udemy Linux Shell Scripting: A Project-Based Approach to Learning by Jason Cannon 




|
