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

WILDCARDS like * star wildcard then so many are there which is helpful in day today task like ? matches exactly one character ??- matches 2 characters
[] matches any one character inside file like ls file[1-3].txt -ouput will be file1 file2 file3 as file1-file3 is already saved in my home directory
[!] matches everything except like ls file[!1].txt will show us all files except file1.txt

&& wildcard controls how command will run together like cp file1.txt && cd file1.txt if first command succeed then only 2nd command will run else nehh
|| or wildcard runs next command only if previous fails
; runs commands no matter what 

|
