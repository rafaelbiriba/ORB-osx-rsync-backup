# OSX Rsync Backup (ORB)

ORB is a RSync script to backup your entire osx disk/partition.

You can also boot from your backup disk/partition (Very useful for test or restore functions).

# INSTALL

Just run the command below to download and give execution permission to ORB script.

    wget https://raw.githubusercontent.com/rafaelbiriba/ORB-osx-rsync-backup/master/orb
    chmod +x orb

# USAGE

## Using default source and destination values

You should edit the `SOURCE` and `DESTINATION` variables at the beginning of `orb` script and then run:

    sudo ./orb

## Using source and destination as parameters

Just run the `orb` script considering first argument `SOURCE` path and second argument `DESTINATION` path.

    sudo ./orb /Volumes/OSX /Volumes/BKP-Disk
