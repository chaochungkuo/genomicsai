---
description: A better option than cp
---

# Archive data with rsync

The typical command for `rsync` is:

```
rsync -av --progress source dest
```

In order to move the data in a safe manner, we need a command which can:&#x20;

* Move the folders with all the files/subfolders within them easily;
* Delete the source files after checking they are copied completely;
* Able to exclude the files by patterns or size

Here I use `find` command first to find whether there are files larger than 100MB which I don't want to archive:

```
find . -type f -size +100M
```

Then I do `rsync` to archive the folders I checked:

```
rsync --remove-source-files -vvv --progress -r --max-size=100M --checksum SOURCE TARGET
```

But `rsync` won't remove the source empty folders, so another command is needed to clean them:

```
find SOURCE -depth -type d -empty -delete
```

For better application of these commands, I put them into one `script archive_folder.sh`:

```bash
#!/bin/bash
# Usage: bash ./archive_folder.sh 
echo "Archiving data from $1 >>>> $2"
echo "**************************************"
SOURCE=$1
TARGET=$1
rsync --remove-source-files -vvv --progress -r --checksum $SOURCE $TARGET
find $SOURCE -depth -type d -empty -delete
```

#### Reference

* [Rsync Show Progress Bar While Copying Files](https://www.cyberciti.biz/faq/show-progress-during-file-transfer/)
* [When is -av NOT the appropriate option for rsync?](https://superuser.com/questions/1322108/when-is-av-not-the-appropriate-option-for-rsync)
* [What is archive mode in rsync?](https://serverfault.com/questions/141773/what-is-archive-mode-in-rsync)
* [Practical Examples of rsync Command in Linux](https://linuxhandbook.com/rsync-command-examples/)
* [RSYNC Does Not Delete Source Directories](https://superuser.com/questions/676671/rsync-does-not-delete-source-directories)
