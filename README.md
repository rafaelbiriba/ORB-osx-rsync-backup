# OSX Rsync Backup (ORB)

ORB is a RSync script to backup your entire osx disk/partition.

You can also boot from your backup disk/partition (Very useful for test or restore functions).

# INSTALL

Just run the command below to download and give execution permission to ORB script.

    wget https://raw.githubusercontent.com/rafaelbiriba/ORB-osx-rsync-backup/master/orb
    chmod +x orb

# USAGE

## Using source and destination as parameters

Just run the `orb` script considering first argument `SOURCE` path and second argument `DESTINATION` path.

    sudo ./orb /Volumes/OSX/ /Volumes/BKP-Disk/

## Using default source and destination values as environment variables

Before execute, you need to export the ORB variables.
`You can just export in shell like the example or export in your `.bashrc`

    $ export ORB_SOURCE='/Volumes/OSX/'
    $ export ORB_DESTINATION='/Volumes/BKP-Disk/'

After export, you can run `orb` command using the parameter `-E env` that give to sudo the access for environment vars.

    $ sudo -E env ./orb

*Hint:* You can export the variables in the root `.bashrc`. With this way, you can run with the command `sudo ./orb` because the exported variable is already accessible from sudo scope.
