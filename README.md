# TYPO3 Legacy Installation with Symlinks using DDEV Local

This repository demonstrates the installation of TYPO3 9.5 with symlinks
according the [Official Documentation](https://docs.typo3.org/m/typo3/guide-installation/9.5/en-us/QuickInstall/GetAndUnpack/Index.html).

The installation steps are done on `ddev start` if TYPO3 is not already setup.
Have a look at the [DDEV Local configuration](.ddev/config.yaml), especially
the post-start hooks which are doing the whole magic.

## How to use

* Install Docker and DDEV Local (and on Windows also Git)
* Download and extract [this repository](https://github.com/GsTYPO3/ddev-typo3-src/archive/master.zip)
* Open a shell, head to the installation folder created before and run `ddev start`

A new browser window opens and shows you the TYPO3 Install Tool. Follow the
installation steps, most of the settings are already preconfigured by DDEV
like the database credentials. Just enter the administrator account and set
a name for the site if you like.

Enjoy!

## Links

* [Install Docker](https://docs.docker.com/#docker-products)
* [Install DDEV Local](https://ddev.readthedocs.io/en/stable/)
* [Install TYPO3 Without Composer](https://docs.typo3.org/m/typo3/guide-installation/9.5/en-us/QuickInstall/GetAndUnpack/Index.html)

## License

This project is released under the terms of the [GNU GENERAL PUBLIC LICENSE](LICENSE)
