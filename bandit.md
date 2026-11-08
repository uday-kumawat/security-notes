Hello everyone my name is uday and i am starting my Cyber Security & Forensics and Ethical Hacking Journey from today.

# day 1 ( Solving Bandit day-1 ) ( 09/11/2026 )

# OverTheWire Bandit Wargame

My personal notes and learning documentation
while completing the OverTheWire Bandit challenges.

Topics covered:
- Linux commands
- File permissions
- SSH authentication
- Networking
- Bash scripting
- Git and GitHub
- Linux privilege management
- Shell environments

# Level 0
On this level i connect bandit from my Linux (Ubuntu) in WSL2  using ssh command and bandit0 as its password on
port number 2220.

command - ssh bandit0@bandit.labs.overthewire.org -p 2220
password - bandit0

# Level 0 -> 1
The password is stord in readme file i use { cat readme } command to see the content of the file and got the
password of next next.

# Level 1 -> 2
The password for next level is storet in file called -located why we can not just use { cat } command on file name
name like this because - ( dash ) is use to give options. so, we have to use it like { cat -- -located } the --
( double dash ) prevents the the CLI to read it as option.

# Level 2 -> 3
Almost same as 2nd level the password in a file called --spaces in this filename-- we use cat '--spaces in this
filename--'. '' ( quotes ) is used so that cat does not treat it as 4 diffrent files.

# Level 3 -> 4
The password for next level is in hidden file called inhere we use { ls } command to see every files and directories
( folder ) in current location ( path )
we use -a to see all the hidden file and folders so, { ls -a } show us the hidden file inhere
we use { cat inhere } to display the password for the next level.
 
# Level 4 -> 5
There is folder called inhere in get into it by use { cd inhere }
then check every file ( from 1 to 10 ) got password in 7th file named --file07.

# Level 5 -> 6
Again as same as previus but with some more precise information of the file. 
we use { find . -type f -size 1033c ! perm /111 }
here find is use to find files and folders and . ( dot ) tells we are going to look for it in same folder.
-type define what are we looking for like file or folder.
-size as per the name we know that it filter out the file and folder by its size.
then finaly we have ! perm /111. perm tell that we are looking file/folder with excatly same perm write
after it like /111 and ! flip it.

# Level 6 -> 7
Same as 5th one we use { find . -user bandit7 -group bandit6 -size 33c } we know about find . and -size.
-user define the owend by which user and same for -group it define owend by which group.

# Level 7 -> 8
We use { grep "millionth" data.txt } the grep command is used to grep word from file.
like in this case we are looking for word "millionth" in file data.txt.

# Level 8 -> 9
Here we use { sort data.txt | uniq -u } this command which mean to sort every live of data.txt by alphabatical order
then use | ( pipe ) to give the output to uniq -q where it displays only lines that appear exactly once.

# Level 9 -> 10  
In this stage we use { strings data.txt | grep "===" } where string extracts readable text from binary data
and pass the output to next command using | ( pipe ) and finaly finds lines containing ===.

# Level 10 -> 11
Base64 is used to Encodes or Decodes the data
and -d enables decoding and data.txt is the file that have encoded data.
we use { base64 -d data.txt } to find password for the next level.

# Level 11 -> 12
The { cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m' } command is used to clear this level
in which { cat data.txt } gives the content of file 
and | ( pipe ) give it to the command { tr } ( Translates characters ) 'A-Za-z' matches all english alphabet letters 
and 'N-ZA-Mn-za-m' rotates each letter by 13 positions.

# Level 12 -> 13
This level involves multiple layers of compression. 
we use { mkdir /tmp/bandit12 } then { cd /tmp/bandit12 } move into this folder
we copy the content file { cp ~/data.txt } then conver hexadump into binery { xxd -r data.txt > decoded } 
then identify the file type by { file decoded }
decompress according to the file type
we have to encounter formats such as, ( gzip → gzip -d ) or ( bzip2 → bzip2 -d ) or ( tar → tar -xf )
until we obtain readable text.

# Level 13 -> 14
This level do not give us password for the next level instead it give SSH private key.
we use { ls } to find sshkey.private in folder then we copy the whole key and exit the ssh 
and creat a file localy called sshkey17
and use it to ssh into next level without password using
{ ssh -i sshkey17 bandit14@bandit.labs.overthewire.org -p 2220 }.
and then we use { cat /etc/bandit_pass/bandit14 } to see password for this level
so, we can ssh into this without very long SSH private key again and again.

# Level 14 -> 15
This level requires sending our current password to a service running on port 30000.
{ cat /etc/bandit_pass/bandit14 | nc localhost 30000 } cat the current password and send to port number 30000 using
nc on localhost means on our machine.

# Level 15 -> 16
This level is similar to the previous one, but uses SSL/TLS encryption.
{ echo "bandit15-Password" | openssl s_client -connect localhost:30001 -quiet }.
The server will return the Bandit 16 password.

# Level 16 -> 17
In this level we have to scan multiple port to check which port is open.
then send current level password to get next level password.
we use { nmap -p 31000-32000 localhost } nmap is a network scanning tool -p 31000-32000 Scans ports in this range
localhost scans your local machine.
we got 5 open port in this stage one reture the password of current level and one will return SSH private key.
using { echo "current-level-password" | openssl s_client -connect localhost:PORT -quiet }
here PORT <- we have to put those 5 port number one by one to check which one is giving SSH keys. 
then copy it localy into a file and ssh into next level to get password using { cat /etc/bandit_pass/bandit17 }.

# Level 17 -> 18
we use { ls }. we see two file called passwords.new and passwords.old there is one line that make difference in
both file.
we use { diff passwords.old passwords.new }.the diff Compares two files - Old password list and updated password list.
the new password is the changed line in passwords.new.

# day 2 ( Solving Bandit day-2 ) ( 10/11/2026 )

# Level 18 -> 19
In this level .bashrc configuration logs you out immediately after login.
instead of opening an interactive shell, run: { ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme }
we'll receive the password for Bandit 19. this is because the shell is non-interactive shells.
learing: SSH can execute a remote command directly without opening a terminal session.

# Level 19 -> 20
we use { la -l } then see bandit20-do after ./bandit20-do we see it will display usage instructions.
{ ./bandit20-do cat /etc/bandit_pass/bandit20 } this executes cat with the permissions of the file owner.
we don't have permission to read /etc/bandit_pass/bandit20 but bandit20-do has the SetUID bit enabled.

# Level 20 -> 21
In this level we have to use two terminals to communicate with each other using a local network connection.
first we use { nc -l -p 1234 } in terminal 1. This command starts a listener on port 1234.
then in terminal 2 we use { ./suconnect 1234 }. This program connects to the listener running on port 1234.
now we send the current level password (Bandit 20 password) through terminal 1.
the suconnect program checks whether the received password is correct. If it matches,
it will return the next level password.

# Level 21 -> 22
In this level we have to find a cron job which is running automatically after a specific time interval.
first we use { ls /etc/cron.d/ } to see the available cron jobs.
then we use { cat /etc/cron.d/cronjob_bandit22 } to check the cron job configuration.
We can see that it runs a script called cronjob_bandit22.sh every minute as bandit22 user.
now we check the script using { cat /usr/bin/cronjob_bandit22.sh }.
inside the script we see that it copies the Bandit 22 password into a temporary file in the /tmp directory.
we use { cat /tmp/bandit22 } to read that file and get the next level password.
learning: { cron jobs, scheduled tasks, shell scripts and temporary files }. 

# Level 22 -> 23
In this level we have to find the password which is stored in a temporary file by a cron job.
first we use { ls /etc/cron.d/ } to find the available cron jobs.
then we check the configuration using { cat /etc/cron.d/cronjob_bandit23 }.
now we check the script using { cat /usr/bin/cronjob_bandit23.sh }.
we can see that the script generates an MD5 hash using the username and stores the password in a file inside 
/tmp directory.
we use { echo I am user bandit23 | md5sum } to generate the same hash.
then we use { cat /tmp/HASH } where HASH is the generated hash value.
this gives us the password for Bandit 23.
learning: MD5 hashing.

# Level 23 -> 24
In this level we have to understand how cron jobs execute scripts automatically.
first we use { ls /etc/cron.d/ } and check the configuration using { cat /etc/cron.d/cronjob_bandit24 }.
then we check the script using { cat /usr/bin/cronjob_bandit24.sh }.
we can see that the cron job executes scripts from the /var/spool/bandit24 directory.
we create our own shell script inside that directory.
the script will read the Bandit 24 password and save it into a temporary file.
we use { nano /var/spool/bandit24/getpass.sh } to create the script.
Inside the script we write:
[
    #!/bin/bash
    cat /etc/bandit_pass/bandit24 > /tmp/bandit24_password
]
then we use { chmod +x /var/spool/bandit24/getpass.sh } to make the script executable.
the cron job automatically executes our script.
after it runs, we use { cat /tmp/bandit24_password } to get the next password.
learning: shell scripting

# Level 24 -> 25
In this level we have to find the correct 4-digit PIN using brute force.
first we connect to the service running on port 30002 using Netcat.
we have to send our current password along with a 4-digit PIN.
there are 10000 possible PIN combinations from 0000 to 9999.
we use a Bash loop to generate all possible combinations and send them to the service.
We use:
[
    password=$(cat /etc/bandit_pass/bandit24)
    for pin in {0000..9999}; do
        echo "$password $pin"
    done | nc localhost 30002
]
The service checks all the combinations and returns the correct password when the PIN matches.
learnig: { brute force, Bash loops, TCP connections and PIN verification }.

# Level 25 -> 26
In this level we have to understand how a restricted login shell works.
We use { ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220 }
when we connect, we see that the shell displays a text file and immediately exits.
this happens because Bandit 26 uses a restricted shell called showtext.
to solve this, we make our terminal window smaller so that the text opens inside the more command.
inside more we press { v } to open the file in Vim.
Then we use:
[
    :set shell=/bin/bash
    :shell
]
This opens a Bash shell.
learning: { restricted shells, Vim and shell environments }.

# Level 26 -> 27
In this level we have to use the same SetUID concept that we learned in Level 19.
after getting access to the Bandit 26 shell, we use { ls } to find an executable called bandit27-do.
we execute it using { ./bandit27-do }. it displays the usage instructions.
then we use { ./bandit27-do cat /etc/bandit_pass/bandit27 }
this executes the cat command with the privileges of the executable owner.
the output gives us the password for Bandit 27.
learning: { SetUID, executable files, Linux permissions and privilege escalation }.

# Level 27 -> 28
In this level we have to work with Git repositories.
first we create a temporary directory using { mkdir /tmp/bandit27 } then { cd /tmp/bandit27 }
then we clone the Git repository using { git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo }
we enter the Bandit 27 password when Git asks for authentication.
after cloning, we enter the repository using { cd repo }. then we use { ls } to see the available files.
we use { cat README } to read the file. the README contains the password for Bandit 28.
learning: { Git, repositories, git clone and README files }.

# Level 28 -> 29
In this level we have to find a password which was removed from a Git repository.
first we create a temporary directory and clone the repository just like the previous level.
{ git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo }
then we enter the repository using { cd repo }.
we use { cat README.md } to check the file. We can see that the password is hidden.
now we use { git log } to check the commit history. we can see that the file was changed in an earlier commit.
we use { git show COMMIT_ID } to inspect the previous version of the file.
the older version contains the password for Bandit 29.
learning: { Git history, git log, git show and previous commits }.

# Level 29 -> 30
In this level we have to find information inside different Git branches.
First we clone the repository { git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo }
then we enter the repository using { cd repo }.
we use { cat README.md } and see that the password is not available in the current branch.
now we use { git branch -a } to list all available branches. we find another branch called dev.
we switch to that branch using { git checkout dev }
then we use { cat README.md } again. the dev branch contains the password for Bandit 30.
learning: { Git branches, git branch, git checkout and branch switching }.

# Level 30 -> 31
In this level we have to find a hidden password inside Git tags.
first we clone the repository { git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo }
then we enter the repository using { cd repo }.we use { git tag } to list all available tags.
we find a tag called secret. now we use { git show secret }
this displays the information stored in that tag.
the output contains the password for Bandit 31.
Here we learn about { Git tags, git show and repository history }.

# Level 31 -> 32
In this level we have to push a file to a remote Git repository.
first we clone the repository { git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo }
then we enter the repository using { cd repo }. we use { cat README.md } to understand the instructions.
we have to create a file called key.txt containing the exact text { May I come in? }
we use { echo "May I come in?" > key.txt } to create the file. now we add the file to Git.
since the file is ignored by .gitignore, we use { git add -f key.txt } the -f option forces Git to add an ignored file.
then we commit the file using { git commit -m "Add key file" }
finally we push the changes using { git push }
the remote repository checks the file and returns the password for Bandit 32.
learning: { Git add, .gitignore, git commit, git push and remote repositories }.

# Level 32 -> 33
In this level we enter a special shell called the uppercase shell.
the shell converts the commands we enter into uppercase, which makes normal Linux commands difficult to execute.
We have to find a way to escape this restricted shell.
We use { $0 }
this executes the shell referenced by the special variable $0 and gives us access to a normal shell.
now we can execute normal Linux commands.
finally we use { cat /etc/bandit_pass/bandit33 }
this displays the final password.
learning: { special shell variables, restricted shells, shell escaping and Linux command execution }.

This is the final level of the Bandit challenge!
