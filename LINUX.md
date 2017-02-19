# Linux

## GENERAL

### History

+ `history` -> show the bash history

+ To define a time format for the history, we can use the `HISTTIMEFORMAT="%d/%m/%y %T"`, you can just write this on the terminal to use just on the current instance or use the
      export HISTTIMEFORMAT="%d/%m/%y %T"
  on our `.zshrc, .bashrc` to save the configuration in all terminal instances.
+   `grep -v "^#" $HISTFILE > /path/file` -> export the bash history to a file.
+ To print the history with the date formated we can use the command: (Tested on the ZSH)
      perl -lne 'm#: (\d+):\d+;(.+)# && printf "%s :: %s\n",scalar localtime $1,$2' $HISTFILE


### SSH

#### Copying files

To copy a file from B to A while logged into B we can use:

      scp /path/to/file username@a:/path/to/destination   
And copy a file from B to A while logged into A:

      scp username@b:/path/to/file /path/to/destination


### Vim

+ `/` or `?` following the word that is searching for -> Find a specific word

+ `:set num` -> Show the line numbers

+ `:%s/foo/bar/g` -> Find each occurrence of 'foo' (in all lines), and replace it with 'bar'.

+ `:%s~<tag />~~g` -> remove all values with the value <tag />

+ `:g/"test"/d` -> remove all line that contains the value "test"


### Files

#### Size

+ `du -h`-> Show the size of the folders recursively
+ `du -hs * | sort -h ` -> Show the size of the folders recursively ordering by size
+ `ls | wc -l` -> Count the number of files in a particular folder

#### Permissions

+ `ls -l` -> Show all folders and files and your permissions
+ `sudo chown -R <user> <folder>`	-> Change files/directory ownership

#### Simbolic links

+ `ln -s /target/directory/file ./shortcut` -> Create a symbolic link

+ `find . -type l -ls` -> Find all simbolic links in the current and subdirectories

#### Lists
+ `find /path/to*.format > files.list` ==> Create a list of all files in a folder with the format specified



### Jobs

To run background jobs we can use the following commands:
+ `CTRL+Z` -> Suspend the current foreground job
+ `bg` -> make the command run in background
+ `jobs` -> See all background jobs
+ `fg` -> Take the most recent background job to the foreground.
+ `fg %1` -> Bring the job#1 to the foreground
+ `kill %2` -> Kill a specific background job, in this case the job #2

### netstat

+ `netstat --listen` -> find open ports

+ `netstat -vatn` -> display open ports and established TCP connections
and if  you want to see FQDN (full dns hostname) try removing the `-n` flag:  `netstat -vat`

+ `netstat -vaun` -> display only open UDP ports

+ `sudo netstat -ltnp | grep ':80'` -> Return which service is using the derminated port.

### Logs
`tail -f ` -> log live preview


## UBUNTU

#### Ubuntu without the GUI
TO run the Ubuntu without the GUI  we need to change (edit) in `/etc/default/grub` file:

From: `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"`
To: `GRUB_CMDLINE_LINUX_DEFAULT="text"`

and save.

And to update the grub configs we need to run on the terminal:
`sudo update-grub`

After reboot, to start the gui just login and type:
`startx`

#### Changing the Ubuntu language

To change the ubuntu language we need to edit the `/etc/default/locale` to the language that we want.
+ eg.:
      LANG="en_US"
      LANGUAGE="en_US:en"

#### PACKAGES

+ `sudo dpkg -i PACKAGE_NAME`	-> install a deb package
+ `sudo dpkg -r PACKAGE_NAME` -> remove a deb package
