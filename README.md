# LinuxCommands
#Author : Aditya Malpani

1. Type of file type:
   - _   regular file
   - d   directory
   - l   link
   - c   special file
   - p   Named pipe 
   - s   socket
   - b   block file

2. Type of file system structure 
   - /boot - used by boot loader
   - /root - root users home directory
   - /dev - system device (disk, keyboard , flashdrive)
   - /etc - configuration file
   - /bin - everyday user command
   - /sbin - system/filesystem command
   - /opt - optional add-on applications
   - /proc - running processes (only exist in memory)
   - /lib - c programming library files needed by applications to run 
   - /tmp - temporary file 
   - /home - directory for users
   - /var - system log
   - /run - system daemons that starts early (eg. systemd  and devd)  to stores temporary running files like PID files
   - /mnt - to mount external filesystem
   - /media - for cdrom mounts

3. find
	```bash 
	find <location> -name <filename>
	```
4. locate - use system database so its faster but newly created files wont be visible 


5. chmod ugo-r  change permissions of the file
	```bash
	chmod ugo+r
	chmod  444 
	chown a+r a for all 
	
	rwx rwx rwx  - user group others
	0 - no permission
	1- execute
	2- write
	3- execute + write
	4- read
	5- read + execute
	6- read + write
	7- read + write + execute
	```
	
6. chown & chgrp  use -R (recursive)
	```bash
	chown/chgrp <user/groupname> <file/directory>
	```

7. ACL (accesscontrol list)
	A perticular user not part of a member of any group created by you but still you want to give some read write access and also dont want to make it a part of group 
	here come ACL 
	commands :  setfacl and getfacl   
	```bash
	setfacl  -m u:username:rwx /path/to/file
	setfacl -m g:groupname:rwx /path/to/file
	setfacl -dm 
	```
	to remove:
	```bash
	setfacl -x 
	```
	example:
	```bash
	setfacl -m u:Nupur:rw abc 
	
		Nupur@aditya-ThinkPad-X220:/tmp$ getfacl abc 
	# file: abc
	# owner: aditya
	# group: aditya
	user::rw-
	user:Nupur:rw-
	group::r--
	mask::rw-
	other::r--
	```
As you assigne the ACL permission to a file/directory it adds + sign at the end of the permission
setting w permission with ACL does not allow to remove file


8. Help command : 
 ```bash
    whatis <command>
    command --help
    man command
 ```

9. Write to the file externally (  > - override , >> - append the in the next line )
    ```bash
	Nupur@aditya-ThinkPad-X220:/tmp$ echo "aditya" > abc 
	Nupur@aditya-ThinkPad-X220:/tmp$ cat abc 
	aditya
	Nupur@aditya-ThinkPad-X220:/tmp$ echo "nupur" > abc 
	Nupur@aditya-ThinkPad-X220:/tmp$ cat abc 
	nupur
	Nupur@aditya-ThinkPad-X220:/tmp$ echo "aditya" >> abc 
	Nupur@aditya-ThinkPad-X220:/tmp$ cat abc 
	nupur
	aditya
    ```

10. tee command:
	```bash
	Nupur@aditya-ThinkPad-X220:/tmp$ echo "aditya & Nupur " | tee -a abc 
	aditya & Nupur 
	Nupur@aditya-ThinkPad-X220:/tmp$ cat abc 
	nupur
	aditya
	aditya & Nupur 
	Nupur@aditya-ThinkPad-X220
	```
		
11. Pipe is used to connect to the output of one command and redirect to input of other command ( | )
	```bash
	lNupur@aditya-ThinkPad-X220:/tmp$ ls -alrth | tail -1    (will give last line)
	-rw-rw-r--+  1 aditya aditya   29 Apr 22 00:26 abc
	Nupur@aditya-ThinkPad-X220:/tmp$ 
	```bash

12.  rm , mv , mkdir , rmdir

13.  cat , more , less  (reverse of more , starts displaying file from last), head ,tail (reverse of head)    --- commands to display file containts

you can use cat command to add content into the file


	```bash
	cat mylinecount.txt | tail -4 |head -2   print line between 6 to 9
	
	aditya@aditya-nupur:~$ cat <<end>> aanu.love
	> hey nuuu
	> end
	aditya@aditya-nupur:~$ cat aanu.love 
	hey nuuu
	aditya@aditya-nupur:\~\$ 
	```


14. cut 

	```bash
	cut -c1 filename
	cur c1,2 filename
	cut -d:  -f 2 filename
	```

15. : awk
	```bash
		awk '{print $1,$3}'  filename
		awk '{print $NF}' filename
		awk '/aditya/ {print}' filename. -search particular string
		awk -F: '{print $1}' cuttest.txt  - : is delimiter
		$echo "hello aditya" | awk '{$2="nupur";print}'  replace aditya with nupur ( can be used in replacing contents of the file

		awk 'length($0) > 15' filename  - --- print lines length more than 15 character
		 awk '{if($1 == "nupur") print $0}' cuttest.txt   -- if first field contains nupur then it will print that line

		awk '{print NF}' cuttest.txt  - print number of columns in each row or line
	```


16. grep 

	```
	grep -c aditya cuttest.txt    number of type aditya occurred
	grep -v aditya cutest.txt    does not match aditya
	grep -i aditya cutest.txt     case insensitive
	egrep -i "aditya|nupur" cuttest.txt  searches either aditya or nupur in the file
	```

17.  sort


	```
		sort cuttest.txt  - will sort and output it to console

		sort -r cuttest.txt  -- reverse sorting

		sort -k2  cuttest.txt  -- sort by second field
	```

18.  uniq


	```bash
		uniq -c adnu.txt

		   2 aditya nupur

		   2 nupur chandak

	```

19. tar -cvf <tarfilename>.tar filetoTar
	
	```bash
	tar xvf <tarfilename>.tar
	```
20.
	
```bash
	gzip abc
	gzip -d abc.gz
```
21.
```bash
	truncate -s 10 aditya,txt - reduce size from end 
```
22. combining and splitting file:
```bash
	cat file1 file2 file3 > file4
	split -l 300 file.txt childfile
```

23.  vi 
   - shift + zz - close file
   - :wq! to close file
   - :q! to close file 
   - :%s/kd//g  -replace all
   - /search 
   - :10 - jump to line number 10
   - :set number - show line number before every line
   - :syntax on - show file in beautiful way
   - :set paste - edit file in paste mode
   - <escape> i - edit mode
   - d - delete   and 10 dd - will delete 10 lines from current line
   - c - copy  and 10 c  -- will copy 10 line from current line
   - p - paste 
   - uu - undo current changes
   - x - delete character
   - . - to repeate same command
   - v- visual mode , you can select strings using movement keys
   - 0 - got to starting character of the line 
   - $ - ending character  of line
   - gg - start of the line
   - shift gg - end of the line

	visual mode 
	c - change selected text ( esc + enter button)
	>	shift right
	<	shift left
	~     switch case ( lower to upper or upper to lower)

Navigation keys
h	moves the cursor one character to the left.
j or Ctrl + J	moves the cursor down one line.
k or Ctrl + P	moves the cursor up one line.
l	moves the cursor one character to the right.
0	moves the cursor to the beginning of the line.
$	moves the cursor to the end of the line.
^	moves the cursor to the first non-empty character of the line
w	move forward one word (next alphanumeric word)
W	move forward one word (delimited by a white space)
5w	move forward five words
b	move backward one word (previous alphanumeric word)
B	move backward one word (delimited by a white space)
5b	move backward five words
G	move to the end of the file
gg	move to the beginning of the file.

Global
:h[elp] keyword - open help for keyword
:sav[eas] file - save file as
:clo[se] - close current pane
:ter[minal] - open a terminal window
K - open man page for word under the cursor
Tip Run vimtutor in a terminal to learn the first Vim commands.
Cursor movement
h - move cursor left
j - move cursor down
k - move cursor up
l - move cursor right
H - move to top of screen
M - move to middle of screen
L - move to bottom of screen
w - jump forwards to the start of a word
W - jump forwards to the start of a word (words can contain punctuation)
e - jump forwards to the end of a word
E - jump forwards to the end of a word (words can contain punctuation)
b - jump backwards to the start of a word
B - jump backwards to the start of a word (words can contain punctuation)
% - move to matching character (default supported pairs: '()', '{}', '[]' - use :h matchpairs in vim for more info)
0 - jump to the start of the line
^ - jump to the first non-blank character of the line
$ - jump to the end of the line
g_ - jump to the last non-blank character of the line
gg - go to the first line of the document
G - go to the last line of the document
5gg or 5G - go to line 5
fx - jump to next occurrence of character x
tx - jump to before next occurrence of character x
Fx - jump to previous occurence of character x
Tx - jump to after previous occurence of character x
; - repeat previous f, t, F or T movement
, - repeat previous f, t, F or T movement, backwards
} - jump to next paragraph (or function/block, when editing code)
{ - jump to previous paragraph (or function/block, when editing code)
zz - center cursor on screen
Ctrl + e - move screen down one line (without moving cursor)
Ctrl + y - move screen up one line (without moving cursor)
Ctrl + b - move back one full screen
Ctrl + f - move forward one full screen
Ctrl + d - move forward 1/2 a screen
Ctrl + u - move back 1/2 a screen
Tip Prefix a cursor movement command with a number to repeat it. For example, 4j moves down 4 lines.
Insert mode - inserting/appending text
i - insert before the cursor
I - insert at the beginning of the line
a - insert (append) after the cursor
A - insert (append) at the end of the line
o - append (open) a new line below the current line
O - append (open) a new line above the current line
ea - insert (append) at the end of the word
Ctrl + h - delete the character before the cursor during insert mode
Ctrl + w - delete word before the cursor during insert mode
Ctrl + j - begin new line during insert mode
Ctrl + t - indent (move right) line one shiftwidth during insert mode
Ctrl + d - de-indent (move left) line one shiftwidth during insert mode
Ctrl + n - insert (auto-complete) next match before the cursor during insert mode
Ctrl + p - insert (auto-complete) previous match before the cursor during insert mode
Ctrl + rx - insert the contents of register x
Esc - exit insert mode
Editing
r - replace a single character
J - join line below to the current one with one space in between
gJ - join line below to the current one without space in between
gwip - reflow paragraph
g~ - switch case up to motion
gu - change to lowercase up to motion
gU - change to uppercase up to motion
cc - change (replace) entire line
C - change (replace) to the end of the line
c$ - change (replace) to the end of the line
ciw - change (replace) entire word
cw - change (replace) to the end of the word
s - delete character and substitute text
S - delete line and substitute text (same as cc)
xp - transpose two letters (delete and paste)
u - undo
U - restore (undo) last changed line
Ctrl + r - redo
. - repeat last command
Marking text (visual mode)
v - start visual mode, mark lines, then do a command (like y-yank)
V - start linewise visual mode
o - move to other end of marked area
Ctrl + v - start visual block mode
O - move to other corner of block
aw - mark a word
ab - a block with ()
aB - a block with {}
at - a block with <> tags
ib - inner block with ()
iB - inner block with {}
it - inner block with <> tags
Esc - exit visual mode
Tip Instead of b or B one can also use ( or { respectively.
Visual commands
> - shift text right
< - shift text left
y - yank (copy) marked text
d - delete marked text
~ - switch case
u - change marked text to lowercase
U - change marked text to uppercase
Registers
:reg[isters] - show registers content
"xy - yank into register x
"xp - paste contents of register x
"+y - yank into the system clipboard register
"+p - paste from the system clipboard register
Tip Registers are being stored in ~/.viminfo, and will be loaded again on next restart of vim.
Tip Special registers:
 0 - last yank
 " - unnamed register, last delete or yank
 % - current file name
 # - alternate file name
 * - clipboard contents (X11 primary)
 + - clipboard contents (X11 clipboard)
 / - last search pattern
 : - last command-line
 . - last inserted text
 - - last small (less than a line) delete
 = - expression register
 _ - black hole register
Marks and positions
:marks - list of marks
ma - set current position for mark A
`a - jump to position of mark A
y`a - yank text to position of mark A
`0 - go to the position where Vim was previously exited
`" - go to the position when last editing this file
`. - go to the position of the last change in this file
`` - go to the position before the last jump
:ju[mps] - list of jumps
Ctrl + i - go to newer position in jump list
Ctrl + o - go to older position in jump list
:changes - list of changes
g, - go to newer position in change list
g; - go to older position in change list
Ctrl + ] - jump to the tag under cursor
Tip To jump to a mark you can either use a backtick (`) or an apostrophe ('). Using an apostrophe jumps to the beginning (first non-black) of the line holding the mark.
Macros
qa - record macro a
q - stop recording macro
@a - run macro a
@@ - rerun last run macro
Cut and paste
yy - yank (copy) a line
2yy - yank (copy) 2 lines
yw - yank (copy) the characters of the word from the cursor position to the start of the next word
y$ - yank (copy) to end of line
p - put (paste) the clipboard after cursor
P - put (paste) before cursor
dd - delete (cut) a line
2dd - delete (cut) 2 lines
dw - delete (cut) the characters of the word from the cursor position to the start of the next word
D - delete (cut) to the end of the line
d$ - delete (cut) to the end of the line
x - delete (cut) character
Indent text
>> - indent (move right) line one shiftwidth
<< - de-indent (move left) line one shiftwidth
>% - indent a block with () or {} (cursor on brace)
>ib - indent inner block with ()
>at - indent a block with <> tags
3== - re-indent 3 lines
=% - re-indent a block with () or {} (cursor on brace)
=iB - re-indent inner block with {}
gg=G - re-indent entire buffer
]p - paste and adjust indent to current line
Exiting
:w - write (save) the file, but don't exit
:w !sudo tee % - write out the current file using sudo
:wq or :x or ZZ - write (save) and quit
:q - quit (fails if there are unsaved changes)
:q! or ZQ - quit and throw away unsaved changes
:wqa - write (save) and quit on all tabs
Search and replace
/pattern - search for pattern
?pattern - search backward for pattern
\vpattern - 'very magic' pattern: non-alphanumeric characters are interpreted as special regex symbols (no escaping needed)
n - repeat search in same direction
N - repeat search in opposite direction
:%s/old/new/g - replace all old with new throughout file
:%s/old/new/gc - replace all old with new throughout file with confirmations
:noh[lsearch] - remove highlighting of search matches
Search in multiple files
:vim[grep] /pattern/ {`{file}`} - search for pattern in multiple files
e.g. :vim[grep] /foo/ **/*
:cn[ext] - jump to the next match
:cp[revious] - jump to the previous match
:cope[n] - open a window containing the list of matches
:ccl[ose] - close the quickfix window
Tabs
:tabnew or :tabnew {page.words.file} - open a file in a new tab
Ctrl + wT - move the current split window into its own tab
gt or :tabn[ext] - move to the next tab
gT or :tabp[revious] - move to the previous tab
#gt - move to tab number #
:tabm[ove] # - move current tab to the #th position (indexed from 0)
:tabc[lose] - close the current tab and all its windows
:tabo[nly] - close all tabs except for the current one
:tabdo command - run the command on all tabs (e.g. :tabdo q - closes all opened tabs)
Working with multiple files
:e[dit] file - edit a file in a new buffer
:bn[ext] - go to the next buffer
:bp[revious] - go to the previous buffer
:bd[elete] - delete a buffer (close a file)
:b[uffer]# - go to a buffer by index #
:b[uffer] file - go to a buffer by file
:ls or :buffers - list all open buffers
:sp[lit] file - open a file in a new buffer and split window
:vs[plit] file - open a file in a new buffer and vertically split window
:vert[ical] ba[ll] - edit all buffers as vertical windows
:tab ba[ll] - edit all buffers as tabs
Ctrl + ws - split window
Ctrl + wv - split window vertically
Ctrl + ww - switch windows
Ctrl + wq - quit a window
Ctrl + wx - exchange current window with next one
Ctrl + w= - make all windows equal height & width
Ctrl + wh - move cursor to the left window (vertical split)
Ctrl + wl - move cursor to the right window (vertical split)
Ctrl + wj - move cursor to the window below (horizontal split)
Ctrl + wk - move cursor to the window above (horizontal split)

24.  sed  command : i flag used to reflect change into the file
   - find and replace on screen :  sed 's/aditya/nupur/g' mylinecount.txt  use i option to reflect changes
   - find and delete : sed -i 's/aditya//g' mylinecount.txt  : used i to reflect changes in file
   - remove lines : sed '/9/d' mylinecount.txt 
   - remove empty lines : sed '/^$/d' mylinecount.txt
   - reomve first line or n line of the file  :  sed '1d' mylinecount.txt 
   - replace tab with space   sed 's/\t/ /g' mylinecount.txt 
   - view specific line : sed -n 12,18p mylinecount.txt 
   - view except specific line : sed 12,18d mylinecount.txt
   - replace all matching except specific line : sed '8!/s/aditya/nupur/' mylinecount.txt

25. useradd: will add entry in cat /etc/passwd ;  cat /etc/shadow (password and )
```bash
	useradd -g groupname -s /bin/bash -m -d /home/nupur nupur
```

26. id :
```bash
	aditya@aditya-ThinkPad-X220:~$ id Nupur
		uid=1001(Nupur) gid=1001(Nupur) groups=1001(Nupur)
	aditya@aditya-ThinkPad-X220:~$
```
27. sudo groupadd family
```bash
	cat /etc/group
```
28 delete user : userdel aditya

29 delete group : groupdel family

30 usermod 
	sudo usermod -G family Nupur   : change users group

31 chgrp 
	chgrp -R family couple

32 : switch users
	su - username
	sudo commands
	file to add in the sudoers list
	/etc/sudoers
33 : monitor users
	who , w, last , finger ,id

34 : talking to users
	command to findout users  -users
	wall <msg>
	write  username <msg>

35 : system utility
	date , uptime , hostname, uname -a , bc (basic calculator) , cal

36: processes and jobs :
	sudo systemctl status mongod - to add it in next boot   systemctl status docker
	ps - show all the processes
	top
	crontab 
	hostnamectl set-hostname aditya-nupur
	kill. -9 thread id

	crontab -- MIN HOUR DOM MON DOW CMD

	Field    Description    Allowed Value
	MIN      Minute field    0 to 59
	HOUR     Hour field      0 to 23
	DOM      Day of Month    1-31
	MON      Month field     1-12
	DOW      Day Of Week     0-6
	CMD      Command         Any command to be executed.

	*/10 * * * *.    ---evert 10 min

	@yearly    0 0 1 1 *
	@daily     0 0 * * *
	@hourly    0 * * * *
	@reboot    Run at startup.

	crontab -e --edit
	crontab -l --- list


	date -s ""  -- set date


37. process management:
    fg
    bg
    nohup process &
    nohup sleep 5 &
    pkill - kill process by name
    nice -  process priority - lower the number more the priority. (nice -n 5 sleep 4)
    top - monitor process
    ps - list of running process


38. system Monitoring:
	df -h - disk partition information
	du  - display disk usage statistics
	dmesg - check if bios issue

	lsof -iTCP -sTCP:LISTEN  check list of open port / files
	free - physical memory
	netstat -rnvl --- check open port
	cat /proc/cpuinfo 
	cat /proc/meminfo 

39. maintenance:
	shutdown
	init 0-6 0- shutdown 1- restart
	reboot 
	halt not waiting for any process (just like pressing powerbutton)

40 finding system info:
	dmidecode
	uname
	difference between 64 - 32 bit - number of calculations per second
	to find it run arch

41 script sessionlog.txt --- will capture whole session - command and command output

42 : environment variable
	env
	to set environment variable -- export test=1
	to set permanent  add in the vi ~/.bashrc  export test=1
	or for all users /etc/.profile pr /etc/.bashrc

43 : 
scripting language
	shell (#!/bash/shell) first line 
	comments #
	commands 
	statements (if , while , for)

	43.1 sample input output:
		aditya@aditya-nupur:~$ cat abc.txt 
		#!/bin/bash
		echo "enter your name nupur"
		read uname
		echo "your name is :" $uname
		aditya@aditya-nupur:~$ 
	
	43.2 if else
		aditya@aditya-nupur:~$ cat ifelse.bash 
		#!/bin/bash
		a=`hostname`
		b=100
		if [ $a == "aditya-nupur" -a $b -eq "100" ]
		then
			echo "hey"$a
		else
			echo "hostname"$a
		fi
		echo "end of code"
		aditya@aditya-nupur:~$ 
		OTHER SYNTAX:	
		if [[ "$stringvar" == *string* ]]; then
		if [[ $num -eq 3 && "$stringvar" == foo ]]; then
		if [ -a existingfile ]   if file exist
		if [ -d directory ]

	43.3 for loops :
		aditya@aditya-nupur:~$ cat forloop.bash 
			#!/bin/bash
			#increment by 2 
			for i in {0..10..2}
			do 
				echo "Welcome $i times"
			done
		aditya@aditya-nupur:~$ 

	43.4 do while script : can use break or continue
	Infinite while Loop
		while :
		do
 		 echo "Press <CTRL+C> to exit."
 		 sleep 1
		done
	-----------------------------------
		i=0
		while [ $i -le 2 ]
		do
		echo Number: $i
		((i++))
		done

	-------------------reading file--------------------------
		file=/etc/passwd
		while read -r line; do
		echo $line
		done < "$file"


	43.5 case 
		syntax:
		case  $variable-name  in
                pattern1|pattern2|pattern3)       
     		    command1
                    ...
                    ....
                    commandN
                    ;;
                pattern4|pattern5|pattern6)
     		    command1
                    ...
                    ....
                    commandN
                    ;;            
                pattern7|pattern8|patternN)       
     		    command1
                    ...
                    ....
                    commandN
                    ;;
                *)              
          esac 
	-------example--------------
			#!/bin/bash
			# if no command line arg given
			# set rental to Unknown
			if [ -z $1 ]
			then
			rental="*** Unknown vehicle ***"
			elif [ -n $1 ]
			then
			# otherwise make first arg as a rental
			rental=$1
			fi

			# use case statement to make decision for rental
			case $rental in
			"car") echo "For $rental rental is Rs.20 per k/m.";;
			"van") echo "For $rental rental is Rs.10 per k/m.";;
			"jeep") echo "For $rental rental is Rs.5 per k/m.";;
			"bicycle") echo "For $rental rental 20 paisa per k/m.";;
			"enfield") echo "For $rental rental Rs.3  per k/m.";;
			"thunderbird") echo "For $rental rental Rs.5 per k/m.";;
			*) echo "Sorry, I can not get a $rental rental  for you!";;
			esac
		-------------------------------------------------
		run it :
		chmod +x rental.sh
		./rental.sh 
		./rental.sh jeep

	
		43.6 program to check remote connectivity ($? exist status of previous command)
			aditya@aditya-nupur:~$ ./remoteconnect.bsh 
				server is up and running
				aditya@aditya-nupur:~$ cat remoteconnect.bsh 
				#!/bin/bash

				ping -c1 172.168.0.109 &> /dev/null

				if [ $? -eq 0 ]
				then
					echo "server is up and running"
				else
					echo "service is down"
				fi
			aditya@aditya-nupur:~$ 
		43.7 special bash parameters and their meaning
			$! bash script parameter is used to reference the process ID of the most recently executed command in background.
			$$ is used to reference the process ID of bash shell itself
			$# is quite a special bash parameter and it expands to a number of positional parameters in decimal.
			$0 bash parameter is used to reference the name of the shell or shell script. so you can use this if you want to print the name of shell script.
			$- (dollar hyphen) bash parameter is used to get current option flags specified during the invocation, by the set built-in command or set by the bash shell itself. Though this bash parameter is rarely used.
			$0 is one of the most used bash parameters and used to get the exit status of the most recently executed command in the foreground. By using this you can check whether your bash script is completed successfully or not.
			$_ (dollar underscore) is another special bash parameter and used to reference the absolute file name of the shell or bash script which is being executed as specified in the argument list. This bash parameter is also used to hold the name of mail file while checking emails.
			$@ (dollar at the rate) bash parameter is used to expand into positional parameters starting from one. When expansion occurs inside double-quotes, every parameter expands into separate words.
			$* (dollar star) this is similar to $@ special bash parameter  only difference is when expansion occurs with double quotes, it expands to a single word with the value of each bash parameter separated by the first character of the IFS special environment variable.
Read more: https://javarevisited.blogspot.com/2011/06/special-bash-parameters-in-script-linux.html#ixzz6LBQASLcG


45 : alias 
		alias pl="pwd ; ls -lrth"
		to check list of alias fire; alias
		ro remove : unalias <aliasname>

46 : history :
		all the command executed will be listed : history 
		to delete history : history -d <linenumber>
		hostory | more
		to execute specific line from history : !<linenumber>


47 Network Files and commands : 
	interface configuration files:
	1. /etc/nsswitch.conf  -- import line : hosts:          files mdns4_minimal [NOTFOUND=return] dns myhostname
	2.  vim /etc/hosts  - mapping of host name and ip address
	3. vim /etc/resolv.conf -- getway info

	Network commands:
		1. ping
		2. ifconfig  -- interfaces and ip details
		3.ifup - to bring up interface
		4.ifdown - to bring down interface
		5. netstate
		5. tcpdump - tcpdump -i <interface name> its basically a snffing tool

48 NIC - Network interface card
	ethtool wlp3s0

	other nics ;
	lo : the loopback device is a special interface that computer uses to communicate with itself.
	used for diagnostics and troubleshooting and to connect to the servers running on the local machine

49 downloading files : (user and password is optional)
	wget --user <username> --password <password> ftp://<ipaddress>/abc.txt
	
50 curl and ping command:
	curl -u -p -o (-o to download like wget)
	ping -c1 www.google.com  (1 packet)

51 FTP :
	sudo systemctl stop vsftpd
	vim /etc/vsftpd.conf
		properties to modify
		anonymous_enable=NO
		ascii_upload_enable=YES
		ascii_download_enable=YES
	how to add file to server
	login to ftp <ipaddress>
		>bi
		>put filename

52 scp secure copy protocol
	scp -r <file/foldername> <username>@<ipaddress>:/<path>

53 rsync-  remote synchronization (based on time and size without or to remote computer) 
	faster than scp and ftp
	used for backup of file 
	default port is 22
	uses ssh protocal
	rsync -rzvh source destination

54 : Telnet and ssh 
	telnet - not secure
	ssh - secure

56 ubuntu firewall :
	sudo ufw status

57 : dns 
	/etc/named.conf
	/var/named
	systemctl start named

58: resolve ip to host or host to ip
		aditya@aditya-nupur:~$ nslookup www.google.com
	Server:		127.0.0.53
	Address:	127.0.0.53#53

	Non-authoritative answer:
	Name:	www.google.com
	Address: 216.58.203.164
	Name:	www.google.com
	Address: 2404:6800:4009:80d::2004

	aditya@aditya-nupur:~$ dig www.google.com

	; <<>> DiG 9.11.3-1ubuntu1.11-Ubuntu <<>> www.google.com
	;; global options: +cmd
	;; Got answer:
	;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 60683
	;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

	;; OPT PSEUDOSECTION:
	; EDNS: version: 0, flags:; udp: 65494
	;; QUESTION SECTION:
	;www.google.com.			IN	A

	;; ANSWER SECTION:
	www.google.com.		231	IN	A	216.58.203.164

	;; Query time: 0 msec
	;; SERVER: 127.0.0.53#53(127.0.0.53)
	;; WHEN: Mon May 04 02:39:29 IST 2020
	;; MSG SIZE  rcvd: 59

	aditya@aditya-nupur:~$

59: ntp : to set time on all te server for time synchronization
	/etc/ntp.conf
	syetemctl status ntp
		ntpq
	ntpq> peers

60: chronyd - replayes ntp 
	/etc/chronyd.conf

61: chage -l aditya
	information about users password
	vim /etc/login.defs  --- where you can define policy or parameters of password
	one more directory to explore for pasword : /etc/pam.d/

62:	to check list of packages
	apt list
	or rpm qa
63: to check list of active services 
	systemctl -a

64: list of ports : 
	netstat -tunlp

65: for more ssh security :
	/etc/ssh/ssh_config
	can cange port
	permit root login

66: enable firegui	
	firewall-config 
	or you can use firewall-cmd to use commandline

67: SELinux - change permission of process

66: to check parameter of the file :
	stat <filename>
	
68 : openldap ; 
	systemctl install slapd
	configuration file: /etc/openldap/slapd.d 

69: tracing network traffic:traceroute
	is used to map a journey that a packet of information undertakes from its source to its destination.
	one use of it is to locate when data loss occurs throughout  a network, which could signify 
	traceroute www.google.com

70 : find gateway :
	 netstat -rnv

71 : access remote machine without password
	sshkey 
	1. sudo ssh-keygen
	copy key generated using above command

	2. copy the key to server
	ssh-copy-id root@<ipaddress>

	3. login from client to server
	ssh -l root <ipaddress>

	you can see keys on server on /root/.ssh/ and cat authorized_keys


72 : 6 different system run level (init 0)
	0 - shutdown 
	1 - single user mode
	6 - reboot 
	2 - mutliuser mode wihtout networking
	3 - mutliuser with networking
	5 - multiuser mode with networking with gui


73 : Linux boot process: 
	BIOS ( looks for where to look boot loder)
	MBR (first sector of the computer (very small in size): Master boot record)
	GRUB (Grant unified bootloader) (which one to choose  kernal images )
	kernel
	init
	Runlevel /etc/rc.d/rc*.d

74: swap : 
used when ram is fulled
inactive page in the memory are moved to swap space

75: execute command in endless loop :
```bash 
	while true; do echo "hi" >> abc.txt ; done
	or 
	# for i in {1..10}; do echo -n "This is a test in loop $i "; date ; sleep 5; done

```

76:Linux command to repeat a string n times 

	1. yes command: to 
```bash
[admalpan]$yes "HelloWorld" | head -n 10
HelloWorld
HelloWorld
HelloWorld
HelloWorld
HelloWorld
HelloWorld
HelloWorld
HelloWorld
HelloWorld
HelloWorld
[admalpan]$
```
	2. print 
```bash 
[admalpan ~]$printf "hi\n%0.s" {1..2}
hi
hi
[admalpan ~]$
```

Netcat without ssh you can log in into other system..

nc -l -p 6996 -e /bin/bash
nc 10.10.10.10 6996

sending file
nc -l -p 8888 > try.txt
cat '/root/try.txt' | nc 10.10.10.10 8888

ssh tunneling: I want to access remote resource..
ssh -L localport:remoteip:port root@remoteip
safe way: 
ssh -nNT -L 9900:localhost:9900 root@remoteip

Remote ssh tunnel : I want ppl access local resource
ssh -R 8888:localhost:8080 root@remotrip


Dynamic port forwarding from work to home as some sites are blocked.
ssh -D 8181 pi@homeip







