protoplc-update
===============

The ProtoPLC Board Support Package (BSP) includes firmware, tools, applications, libraries and supporting documentation. The `protoplc-update` tool updates the ProtoPLC BSP from your Raspberry Pi.

## Installing

To install the tool, run the following command on the Raspberry Pi:

    sudo curl -L --output /usr/bin/protoplc-update https://raw.github.com/mobileappsystems/protoplc-update/master/protoplc-update && sudo chmod +x /usr/bin/protoplc-update

## Updating

Then to update your ProtoPLC firmware and SDK, just run the following command:

    sudo protoplc-update

## Activating

After the firmware and SDK have been sucessfully updated, the ProtoPLC board is re-programmed and automatically rebooted. There is no need to reboot your Raspberry Pi.

## Options

The SDK is updated to the latest version. To upgrade/downgrade the firware to a specific revision, specify its Git hash (from the `https://github.com/mobileappsystems/protoplc-firmware` repository) as follows:

    sudo protoplc-update 55ae4046186027f4d961dcd48259fbb88cf1f161


### Expert options

There are a number of options for experts you might like to use. These are all environment variables you must set if you wish to use them.

#### `UPDATE_SELF`

    sudo UPDATE_SELF=0 protoplc-update

By default, `protoplc-update` will attempt to update itself each time it is run. The above disables this behaviour.

#### `SKIP_BACKUP`

    sudo SKIP_BACKUP=1 protoplc-update

Avoids making backup of `/usr/local/mas/protoplc` to `/usr/local/mas/protoplc.bak`

#### `SKIP_REPODELETE`

    sudo SKIP_REPODELETE=1 protoplc-update

By default the downloaded files (`/root/.protoplc-firmware` and `/root/.protoplc-sdk`) are deleted at the end of an update. Using this option avoids deleting the files.

#### `ROOT_PATH` and `MAS_PATH`

    sudo ROOT_PATH=/media/root MAS_PATH=/media/usr/local/mas protoplc-update

Allows you to perform an *offline* update to an SD card you are not currently booted from. Be careful, you must specify both options or neither. Specifying only one will not work.

#### `BRANCH`

By default, `protoplc-update` will clone files from the `master` branch. Specifying a branch as follows:

    sudo BRANCH=develop protoplc-update

will use the `develop` branch instead.

## Troubleshooting

There are two possible problems related to SSL certificates that may prevent this tool from working.

-   The time may be set incorrectly on your Raspberry Pi, which you can fix
    by setting the time using NTP.

        sudo apt-get install ntpdate
        sudo ntpdate -u ntp.ubuntu.com

-   The other possible issue is that you might not have the `ca-certificates`
    package installed, and so GitHub's SSL certificate isn't trusted. If you are
    on Debian, you can resolve this by typing:

        sudo apt-get install ca-certificates

## Software License

`protoplc-update` is free software distributed under the terms of the [MIT license](http://www.opensource.org/licenses/mit-license.html) reproduced in the included LICENSE file.
