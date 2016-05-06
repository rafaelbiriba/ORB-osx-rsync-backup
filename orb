#!/bin/bash

# OSX Rsync Backup (ORB)
#
# ORB is a RSync script to backup your entire osx disk/partition.
# You can also boot from your backup disk/partition (Very useful for test or restore functions).
#
# Created by: Rafael Biriba - biribarj@gmail.com
# More info: https://github.com/rafaelbiriba/ORB-osx-rsync-backup

# USAGE: (With inline parameters)
# $ sudo ./orb /Volumes/OSX-Source/ /Volumes/OSX-Destination/

# USAGE: (With local environment variables)
# $ export ORB_SOURCE='/Volumes/OSX-Source/'
# $ export ORB_DESTINATION='/Volumes/OSX-Destination/'
# $ sudo -E env ./orb

SCRIPT_USAGE="\n
USAGE: (With inline parameters)
\n
$ sudo ./orb /Volumes/OSX-Source/ /Volumes/OSX-Destination/
\n\n
USAGE: (With local environment variables)
\n
$ export ORB_SOURCE='/Volumes/OSX-Source/'
\n
$ export ORB_DESTINATION='/Volumes/OSX-Destination/'
\n
$ sudo -E env ./orb
\n\n"

if [ -n "$1" ] && [ -n "$2" ]; then
  SOURCE=${1%/}
  DESTINATION=${2%/}
fi

if [ -n "$ORB_SOURCE" ] && [ -n "$ORB_DESTINATION" ]; then
  SOURCE=${ORB_SOURCE%/}
  DESTINATION=${ORB_DESTINATION%/}
fi

if ! [ -n "$SOURCE" ] && ! [ -n "$DESTINATION" ]; then
  echo -e $SCRIPT_USAGE
  exit;
fi

echo -e "\n"
echo -e "Starting ORB backup script...\n"

# Make sure only root can run the script
if [[ $EUID -ne 0 ]]; then
   echo -e "Aborting the sync process: This script must be run as root\n"
   exit;
fi

if [ ! -r "$SOURCE" ]; then
    echo -e "Aborting the sync process: Source '$SOURCE/' not readable\n"
    exit;
fi

if [ ! -w "$DESTINATION" ]; then
    echo -e "Aborting the sync process: Destination '$DESTINATION/' not writeable\n"
    exit;
fi

echo -e "Check the selected folders:"
echo -e "Source folder: $SOURCE/"
echo -e "Destinantion folder: $DESTINATION/"
echo -e "Waiting 5 seconds before continue. [Control+C] to cancel the execution if something is wrong..."
sleep 5
echo -e "Executing..."

rsync  --acls \
       --archive \
       --delete \
       --delete-excluded \
       --hard-links \
       --one-file-system \
       --sparse \
       --verbose \
       --xattrs \
       --times \
       --crtimes \
       --human-readable \
       --progress \
       --perms \
       --executability \
       --owner \
       --group  \
       --exclude '.Spotlight-*' \
       --exclude '.Trashes' \
       --exclude '/afs/*' \
       --exclude '/automount/*' \
       --exclude '/cores/*' \
       --exclude '/dev/*' \
       --exclude '/Network/*' \
       --exclude '/private/tmp/*' \
       --exclude '/private/var/run/*' \
       --exclude '/private/var/spool/postfix/*' \
       --exclude '/private/var/vm/*' \
       --exclude '/Previous Systems.localized' \
       --exclude '/tmp/*' \
       --exclude '/Volumes/*' \
       --exclude '*/.Trash' \
       "$SOURCE"/ "$DESTINATION"/

bless --folder "$DESTINATION"/System/Library/CoreServices

exit 0
