# TYPO3 Legacy Installation with Symlinks using DDEV Local

This repository demonstrates the installation of TYPO3 with symlinks
according the [Official Documentation](https://docs.typo3.org/m/typo3/guide-installation/master/en-us/QuickInstall/GetAndUnpack/Index.html).

The installation steps are done on `ddev start` if TYPO3 is not already setup.
Have a look at the [DDEV Local configuration](.ddev/config.yaml), especially
the post-start hooks which are doing the whole magic.

## How to use

* Install Docker and DDEV Local (and on Windows also Git)
* Download and extract [this repository](https://github.com/GsTYPO3/ddev-typo3-src/archive/master.zip)
* [optional] Edit `[installation-folder]/.ddev/config.yaml` to your likings
* Open a shell, head to the installation folder created before and run `ddev start`

Please note there are various branches for all TYPO3 versions since 6.2.

A new browser window opens and displays the TYPO3 Install Tool. Follow the
installation steps, most of the settings are already preconfigured by DDEV
like the database credentials. Just enter the administrator account credentials
and set a name for the site if you like.

Enjoy!

## Configuration

Each branch defines the `TYPO3_MAJOR_VERSION` variable. The install script
fetches the last release of this major version directly from `get.typo3.org`.

It's also possible to install a specific release by defining `TYPO3_SRC_VERSION`
in the `config.yaml` instead. `TYPO3_MAJOR_VERSION` is ignored in this case.

The default web / document root is set to `htdocs` which can be changed in the
`config.yaml` to reflect your production server.

Also `PHP` and `Database` version can be changed in the `config.yaml`.

To avoid side effects please adapt the configuration **before** the first
`ddev start`.

## Windows and Symlinks

To create and show the symlinks correctly on Windows you have to enable the
Developer Mode or start your shell (Git Bash, cmd, PowerShell etc.) elevated
(as adminstrator).

Otherwise the linked folders and files are shown as regular text files with some
information about the target inside. This does not hurt the functionality,
container but could be a little bit confusing on the host side if you
are not awarae of this behavior.

## Links

* [Install Docker](https://docs.docker.com/#docker-products)
* [Install DDEV Local](https://ddev.readthedocs.io/en/stable/)
* [Install TYPO3 Without Composer](https://docs.typo3.org/m/typo3/guide-installation/9.5/en-us/QuickInstall/GetAndUnpack/Index.html)

## License

This project is released under the terms of the [GNU GENERAL PUBLIC LICENSE](LICENSE)
