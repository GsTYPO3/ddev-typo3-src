# TYPO3 Legacy Installation with Symlinks using DDEV Local

This repository demonstrates the installation of TYPO3 with symlinks
according the [Official Documentation](https://docs.typo3.org/m/typo3/guide-installation/master/en-us/QuickInstall/GetAndUnpack/Index.html).

The installation steps are done on `ddev start` if TYPO3 is not already setup.
Have a look at the [DDEV Local configuration](.ddev/config.yaml), especially
the post-start hooks which are doing the whole magic.

## How to use

* Install Docker and DDEV Local (and on Windows also Git)
* Download and extract this repository (see links below)
* [optional] Edit `[project-root-folder]/.ddev/config.yaml` to your likings
* Open a shell, head to the installation folder created before and run `ddev start`

A new browser window opens and displays the TYPO3 Install Tool. Follow the
installation steps, most of the settings are already preconfigured by DDEV
like the database credentials. Just enter the administrator account credentials
and set a name for the site if you like.

Please note there are various [branches](branches) for all TYPO3 versions since
6.2. Each branch is preconfigured to the latest supported components like PHP
and MariaDB:

* [Download](archive/refs/heads/main.zip) for TYPO3 11.5
* [Download](archive/refs/heads/10.4.zip) for TYPO3 10.4
* [Download](archive/refs/heads/9.5.zip) for TYPO3 9.5
* [Download](archive/refs/heads/8.7.zip) for TYPO3 8.7
* [Download](archive/refs/heads/7.6.zip) for TYPO3 7.6
* [Download](archive/refs/heads/6.2.zip) for TYPO3 6.2

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
are not aware of this behavior.

## Upgrade

If you want to upgrade your TYPO3 version, please take all the information into
consideration that the offical upgrade guide recommends: [Upgrading TYPO3](https://docs.typo3.org/m/typo3/guide-installation/master/en-us/).

Here are all the steps to be considered in a nutshell:

* Update all third-party extensions to their latest possible version
* Deactivate all third-party extensions
* ⚠️ Export and backup the current database with: `ddev export --file=db_backup.sql`
* Stop the project with `ddev stop`
* Remove `htdocs/typo3temp`
* Adapt the settings in `.ddev/config.yaml` to your new [requirements](https://get.typo3.org):
  * `php_version`
  * `mariadb_version` / `mysql_version`
  * `TYPO3_MAJOR_VERSION` / `TYPO3_SRC_VERSION`
* Run `ddev start`
* Login to the install tool
* Run TYPO3's `Upgrade Wizard`: "Upgrade -> Upgrade Wizard"
* Switch to the backend
* Update extension list in "Admin Tools -> Extensions -> [dropdown] Get
  Extensions -> Update now"
* Update third-party extensions
* Activate third-party extensions again

### Upgrade Troubleshooting

In case you experience troubles with the update, you might want to check things
like these:

* Have all third-party etensions been deactivated? If not, check the file
  `typo3conf/PackageStates.php` and delete all entries that point to a
  third-party extension. (If this was something you had to do, you might also
  want to check, if the folder `typo3temp` still exists and, if so, delete it)
* Delete all files in `.ddev` except `config.yaml` and run `ddev start` again
* If you have developed your own custom extensions, make sure to adjust the
  version dependencies in `ext_emconf.php` in case you have defined any
* In case the database has been completely overwritten:
  * Check, if database has been completely overwritten by opening the backend
    and trying to log in. If you cannot log in, the user has been deleted. (You
    can also check the database status with `ddev sequelace`, if you are on a Mac)
  * Import your database backup with: `ddev import --src=db_back.sql`
  * Run TYPO3's database compare: "Admin Tools -> Maintenance -> Analyze
    Database Structure"

## Support for local extensions

If you would like to implement local extensions, a composer-like setup is
supported. All you have to do is create a folder for your local extensions at
the root level (default `packages`) and copy your local extensions to this
folder where each subfolder is an extension.

To use a folder other than `packages` overwrite the default with the variable
`TYPO3_LOCAL_EXTENSIONS` in `.ddev/config.yaml` under the `web_environment` key:

```yaml
web_environment:
- TYPO3_LOCAL_EXTENSIONS=[your-folder-name]
```

## Links

* [Install Docker](https://docs.docker.com/#docker-products)
* [Install DDEV Local](https://ddev.readthedocs.io/en/stable/)
* [Install TYPO3 Without Composer](https://docs.typo3.org/m/typo3/guide-installation/9.5/en-us/QuickInstall/GetAndUnpack/Index.html)

## License

This project is released under the terms of the [GNU GENERAL PUBLIC LICENSE](LICENSE)
