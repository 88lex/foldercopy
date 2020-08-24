### Foldercopy - quick copy utility for Google Team/Shared Drives with string matches, using rclone

- `folderlist` generates a static list of all folders in selected directories in Drive.
- `foldercopy` copies folders matching any string to a destination folder using source-destination pairs in a set file.
- `foldercopy2` copies folders matching any string to a folder you designate in the command line.
- `foldercopy` and `foldercopy2` display a list of matching folders and require confirmation before copying (by default)


Syntax: 
  - `./foldercopy tv Bananas` will copy any folders that include the string `Bananas` (ignore caps) between folders defined in the set `tv`
  - `./foldercopy tv Bananas 2007` will copy any folders that include the strings `Bananas` and `2007`
  - `./foldercopy2 tv my_remote:comedy Bananas` will copy any folders that include the string `Bananas` to the `my_remote:comedy` folder
  - `./folderlist tv` generates a static list of all folders that are in the set file `tv`, so searches are instant and copying can begin without scanning

  - Folders can be mapped with files in the `/sets` folder. For example a file `/sets/tv` could contain
```
        my_td:video         bak_td:video
        my_td:documentary   bak_td:documentary
        my_td:nature        bak_td:nature
```
  - `./folderlist tv` will generate a list of all folders in my_td:video , documentary and nature as well as a mapping of all folders to bak_td:. These lists are saved in `/src_folders` and `src_dest_folders` directories.


