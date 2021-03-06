### Foldercopy - quick copy utility for Google Team/Shared Drives with string matches, using rclone (or lclone or gclone)

  - `foldercopy` copies folders matching any `filter`

  - foldercopy also copies shortcuts for folders using `./shcut set_name filter`

NOTE: `foldercopy` requires a local list of folders. Create a set in `/sets/` and run `./folderlist set_name` to generate / update your list(s). The file is stored in `/src_folders` and can be updated as often as needed.


Syntax: 
  - `./folderlist tv` generates a file listing all folders in the source remotes in the set file `tv`. Subsequent searches are instant and copying can begin without re-scanning the remote.
  - `./foldercopy tv Bananas` will copy any folders that include the string `Bananas` (ignore caps) between folders defined in the set file called `tv`
  - `./foldercopy tv Bananas 2007` will copy any folders that include the strings `Bananas` and `2007`
  - `./foldercopy -d my_remote:comedy tv Bananas` will copy any folders that include the string `Bananas` to the `my_remote:comedy` folder
  - flags must come before the set name. `./foldercopy tv Bananas -d my_remote:comedy` will NOT work 

  - After running a command foldercopy will give you a list and a choice
    - `y` to copy/sync/move all folders listed.
    - `n` to abort
    - `s` to select one of the folders shown in the list
    - `c` to change or refine the filter 

  - Folder `sets` map the source and destination pairs in files in the `/sets` folder. These pairs can be as simple or complex as you like. For example a file `/sets/tv` could contain
```
        my_td:video         bak_td:video
        my_td:documentary   bak_td:documentary
        my_td:nature        bak_td:nature
```
  - `./folderlist tv` will generate a list of all folders in my_td:video , documentary and nature as well as a mapping of all folders to bak_td:. These lists are saved in `/src_folders` and `src_dest_folders` directories.
  - There is a `config` file with a number of basic settings for default folders, actions, etc.
  - Many settings use flags, and some have short command alternatives. Most short commands accept flags:
```
      FLAG      OR   COMMAND
      -c|--copy)     fcopy    => copy (This is the default action)
      -m|--move)     fmove    => move
      -s|--sync)     fsync    => sync
      -z|--shcut)    shcut    => create shortcuts of the source folders
                     fcomp    => compare two folder lists
                     listsets => shows all of your set files. Select to print contentss
      -r|--rclone             => use rclone (This is the default app for copying)
      -l|--lclone)            => use lclone
      -g|--gclone)            => use gclone
      -a|--auto)              => copy without user confirmation    
      -t|--test)              => print command with executing
      -d|--dest)              => set destination manually (e.g. -d remote:folder)
      -f|--flag)              => add a flag to rclone. Each flag requires -f: `-f --flag1 -f flag2`
      -u|--update)            => update folderlist, then run filter and other commands
```
  - `foldercopy` works with rclone, gclone and lclone (l3uddz's rclone_gclone fork). This can be set in the `config` file or with flags
  - `./listcopy 
  - `./fcomp set1 set2` creates a file in src_folders listing folders in set1 that are not in set2. `fcomp` will then ask if you want to copy (or sync or move) those folders.


HINTS:
- searches can use partial and multiple filters
  - e.g You have a folderlist called `videos` which includes a folders called /holiday/2014/italy and /holiday/2015/japan
  - `./fcopy videos hol 14` will find `/holiday/2014/italy`
  - `./fcopy videos 201` will find `/holiday/2014/italy` and `/holiday/2015/japan`
  - `./fcopy videos 2014 holiday` will find nothing, as the holiday precedes 2014 in the string
