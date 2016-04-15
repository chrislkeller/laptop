Keller's Kool Laptop
====================

~~[![Build Status](https://travis-ci.org/18F/laptop.svg)](https://travis-ci.org/18F/laptop)~~

Laptop is a script to set up an OS X computer for web development.

It can be run multiple times on the same machine safely.
It installs, upgrades, or skips packages
based on what is already installed on the machine.

Requirements
------------

Tested:

* [OS X El Capitan (10.11)](https://www.apple.com/osx/)

Older versions may work but aren't regularly tested. Bug reports for older versions are welcome.

Performing Clean Install
------------------------

* [Create Bootable OS X USB Installation Drive](http://www.macworld.com/article/2367748/how-to-make-a-bootable-os-x-10-10-yosemite-install-drive.html)
    * Download ~~OS X Yosemite~~ the latest OS upgrade from the Mac App Store
    * With a USB drive > 8GB, open Disk Utility and select the drive in the sidebar
    * Format the drive as "Mac OS Extended (Journaled)" and name it "Untitled"
    * The installer should be in your Applications folder
    * [Run the following from the CLI](http://forums.macrumors.com/showpost.php?p=18081307&postcount=3) and "wait about 20 minutes"

            sudo /Applications/<name-of-installer>/Contents/Resources/createinstallmedia --volume /Volumes/Untitled --applicationpath /Applications/<name-of-installer> --nointeraction

    * You should see something like this:

            Erasing Disk: 0%... 10%... 20%... 100%...
            Copying installer files to disk...
            Copy complete.
            Making disk bootable...
            Copying boot files...
            Copy complete.
            Done.

    * When it's done, you should get a message stating the process is finished
    * Restart your computer and hold the Option key to access the boot menu
    * Select your new USB drive to install a clean copy of OS X Yosemite

After The Clean Install
-----------------------

Begin by opening the Terminal application on your Mac. The easiest way to open
an application in OS X is to search for it via [Spotlight](https://support.apple.com/en-us/HT204014). The default keyboard shortcut for invoking Spotlight is `command-Space`. Once Spotlight is up, just start typing the first few letters of the app you are looking for, and once it appears, press `return` to launch it.

* Uninstall any existing development tools

        sudo /Developer/Library/uninstall-devtools

* Skip XCode and go for the Command Line Tools for XCode. It's much faster than installing the whole XCode suite, which is huge and I don't do anything with it. I will miss the iOS simulators though.

    * More on this method [here](http://www.bloggure.info/work/installing-homebrew-without-xcode.html).

    * Run the following from your terminal

            ```sh
            xcode-select --install
            ```

    * You'll get a prompt to "Get Xcode", "Cancel", or "Install". Skip installing the entire Xcode application. Choose install to get the Command Line Tools.

    * If the above errors out, you can download [Command Line Tools for XCode](https://developer.apple.com/downloads/index.action). Then open the Command Line Tools for XCode dmg and install.

* Unfurl the Setup Script

    * Proceed using a script based on the work shown in [Laptop](https://github.com/thoughtbot/laptop/blob/master/README.md), a version used by [The Associated Press](https://github.com/associatedpress/laptop) and a version used by [18F](https://github.com/18F/laptop).

    * In your Terminal window, copy and paste each of these three commands one at a time, then press `return` after each one. The first two commands download the files the script needs to run, and the third command executes the script.

    * Download the scripts from the GitHub repository and run them

            ```sh
            curl --remote-name https://raw.githubusercontent.com/chrislkeller/laptop/master/mac
            curl --remote-name https://raw.githubusercontent.com/chrislkeller/laptop/master/Brewfile
            curl --remote-name https://raw.githubusercontent.com/chrislkeller/laptop/master/.laptop.local
            bash mac 2>&1 | tee ~/Desktop/laptop.log
            ```

    * The [script](https://github.com/chrislkeller/laptop/blob/master/mac) itself is available in this repo for you to review if you want to see what it does and how it works.

    * Note that the script will ask you to enter your OS X password at various points. This is the same password that you use to log in to your Mac.

    * **Once the script is done, make sure to quit and relaunch Terminal.**

            ```sh
            source ~/.bash_profile
            ```

    * More [detailed instructions with a video](https://github.com/18F/laptop/wiki/Detailed-installation-instructions-with-video) are available in the Wiki.

Debugging
---------

Your last Laptop run will be saved to `~/Desktop/laptop.log`. Read through it to see if you can debug the issue yourself. If not, copy and paste the entire log into a [new GitHub Issue](https://github.com/18F/laptop/issues/new) for us.

What's being set up
-------------------

* Create your ```.bashrc```.
* Install, update and check [homebrew](http://mxcl.github.com/homebrew/) for managing packages.
* Configure ```$PATH``` variables for homebrew
* Install [homevbrew-cask](https://github.com/caskroom/homebrew-cask) for managing native applications.
* Install homebrew versions of ```node.js``` and ```npm```
* Update ```Ruby```, install ```rvm```, update ```gems```, install ```bundler``` and ```capistrano```
    * rvm install 1.9.3 --with-gcc=clang
* Install homebrew versions of ```python```, ```python3```, ```pip```, ```virtualenv``` and ```virtualenvwrapper```
* Upgrade ```setuptools``` and ```distribute```
* Configure ```$PATH``` variables for ```virtualenv```
* install csvkit and agate
* Configure ```$PATH``` variables for ```rvm```
* Install MySQL and start at login
* Install Postgres and PostGIS
    * These links helped with the Postgres install
        * [To create a spatially-enabled database](http://postgis.net/docs/manual-2.1/postgis_installation.html#create_new_db_extensions)
        * [Users of 1.5 and below will need to go the hard-upgrade path, see here](http://postgis.net/docs/manual-2.1/postgis_installation.html#upgrading)
        * PostGIS SQL scripts installed to ```/usr/local/share/postgis```
        * PostGIS plugin libraries installed to ```/usr/local/opt/postgresql/lib```
        * PostGIS extension modules installed to ```/usr/local/opt/postgresql/share/postgresql/extension```
* Install QGIS 2.8





    * alias db-load='cd ~/_programming/_mach_dotfiles/shell-scripts && py ~/_programming/_mach_dotfiles/shell-scripts/db-load.py'

    * source ~/.bash_profile
    * slime ~/programming

    * Install IE vms

            ```curl -s https://raw.githubusercontent.com/xdissent/ievms/master/ievms.sh | env IEVMS_VERSIONS="8 9 10 11" INSTALL_PATH="/Volumes/one_tb_hd/virtualbox_vms/ie_vms" bash```

        * You may remove all files except *.vmdk after installation and they will be re-downloaded if ievms is run again in the future:

            ```$ find ~/.ievms -type f ! -name "*.vmdk" -exec rm {} \;```

        * Copy And Paste Between [VirtualBox Host And Guest Machines](https://www.liberiangeek.net/2013/09/copy-paste-virtualbox-host-guest-machines/)

        * Access host localhost by going to [http://10.0.2.2:8880](http://10.0.2.2:8880) on the guest

        * Misc
            * Download [AppCleaner](http://www.freemacsoft.net/appcleaner/) and get rid of some cruft if you want.
                * Or delete from the command line

                        cd /Applications/
                        sudo rm -rf Stickies.app/
                        sudo rm -rf Chess.app/
                        sudo rm -rf Photo\ Booth.app











* [CloudApp] for sharing screenshots and making an animated GIF from a video
* [Cloud Foundry CLI] for command line access to 18F's Cloud Foundry-based application platform
* [Flux] for adjusting your Mac's display color so you can sleep better
* [GitHub Desktop] for setting up your SSH keys automatically
* [Homebrew] for managing operating system libraries
* [Homebrew Cask] for quickly installing Mac apps from the command line
* [Homebrew Services] so you can easily stop, start, and restart services
* [hub] for interacting with the GitHub API
* [ImageMagick] for cropping and resizing images
* [MySQL] for storing relational data
* [n] for managing Node.js versions if you do not have [Node.js] already installed (Includes latest [Node.js] and [NPM], for running apps and installing JavaScript packages)
* [PhantomJS] for headless website testing
* [Postgres] for storing relational data
* [pyenv] for managing Python versions if you do not have [Python] already installed (includes the latest 3.x [Python])
* [Redis] for storing key-value data
* [RVM] for managing Ruby versions (includes [Bundler] and the latest [Ruby])
* [Slack] for communicating with your team
* [Sublime Text 3] for coding all the things
* [The Silver Searcher] for finding things in files
* [Virtualenv] for creating isolated Python environments (via [pyenv] if it is installed)
* [Virtualenvwrapper] for extending Virtualenv (via [pyenv] if it is installed)
* [Zsh] as your shell

[Bundler]: http://bundler.io/
[CloudApp]: http://getcloudapp.com/
[Cloud Foundry CLI]: https://github.com/cloudfoundry/cli
[Flux]: https://justgetflux.com/
[GitHub Desktop]: https://desktop.github.com/
[Homebrew]: http://brew.sh/
[Homebrew Cask]: http://caskroom.io/
[Homebrew Services]: https://github.com/Homebrew/homebrew-services
[hub]: https://github.com/github/hub
[ImageMagick]: http://www.imagemagick.org/
[MySQL]: https://www.mysql.com/
[n]: https://github.com/tj/n
[Node.js]: http://nodejs.org/
[NPM]: https://www.npmjs.org/
[PhantomJS]: http://phantomjs.org/
[Postgres]: http://www.postgresql.org/
[Python]: https://www.python.org/
[pyenv]: https://github.com/yyuu/pyenv/
[Redis]: http://redis.io/
[Ruby]: https://www.ruby-lang.org/en/
[RVM]: https://github.com/wayneeseguin/rvm
[Slack]: https://slack.com/
[Sublime Text 3]: http://www.sublimetext.com/3
[The Silver Searcher]: https://github.com/ggreer/the_silver_searcher
[Virtualenv]: https://virtualenv.pypa.io/en/latest/
[Virtualenvwrapper]: http://virtualenvwrapper.readthedocs.org/en/latest/#
[Zsh]: http://www.zsh.org/



----

Load up bak MySQL databases
---------------------------

```setup-dbload.py``` is an example python script to - given a directory of .sql files - load them one by one into a local MySQL instance. It assumes ```MySQLdb``` has been installed via pip or another python package manager.

Load up bak virtualenvs
-----------------------

```setup-requirements.sh``` is an example shell script to - given a directory of virtualenv requirements.txt files - load them one by one into a specific virtualenv. It assumes ```virtualenv``` and ```virtualenvwrapper``` has been installed via pip or another python package manager.

----






Customize in `~/.laptop.local` and `Brewfile`
---------------------------------------------

Your `~/.laptop.local` is run at the end of the `mac` script.
Put your customizations there. This repo already contains a `.laptop.local`
you can use to get started.

```sh
# Go to your OS X user's root directory
cd ~

# Download the sample file to your computer
curl --remote-name https://raw.githubusercontent.com/18F/laptop/master/.laptop.local
```

It lets you install the following tools:

* [Atom] - GitHub's open source text editor
* [Exuberant Ctags] for indexing files for vim tab completion
* [Firefox] for testing your website on a browser other than Chrome
* [iTerm2] - an awesome replacement for the OS X Terminal
* [reattach-to-user-namespace] to allow copy and paste from Tmux
* [Tmux] for saving project state and switching between projects
* [Vim] for those who prefer the command line

[Atom]: https://atom.io/
[Exuberant Ctags]: http://ctags.sourceforge.net/
[Firefox]: https://www.mozilla.org/en-US/firefox/new/
[iTerm2]: http://iterm2.com/
[reattach-to-user-namespace]: https://github.com/ChrisJohnsen/tmux-MacOSX-pasteboard
[Tmux]: http://tmux.sourceforge.net/
[Vim]: http://www.vim.org/

For example:

```sh
#!/bin/sh

fancy_echo "Running your customizations from ~/.laptop.local ..."

brew bundle --file=- <<EOF
cask 'atom'
cask 'firefox'
cask 'iterm2'

brew 'vim'
brew 'ctags'
brew 'tmux'
brew 'reattach-to-user-namespace'

brew 'go'
EOF

append_to_file "$HOME/.zshrc" 'export PATH="$PATH:/usr/local/opt/go/libexec/bin"'
```

Write your customizations such that they can be run safely more than once.
See the `mac` script for examples.

Laptop functions such as `fancy_echo` and `gem_install_or_update` can be used
in your `~/.laptop.local`.

Editing the `Brewfile`
----------------------
Most of what the script installs is listed in the `Brewfile`. If you don't want
the script to install certain tools, you can remove them from the `Brewfile`.


How to manage background services (Redis, Postgres, MySQL)
----------------------------------------------------------
The script does not automatically launch these services after installation
because you might not need or want them to be running. With Homebrew Services,
starting, stopping, or restarting these services is as easy as:

```
brew services start|stop|restart [name of service]
```

For example:

```
brew services start redis
```

To see a list of all installed services:

```
brew services list
```

To start all services at once:

```
brew services start --all
```

Credits
-------

Keller's Kool Laptop script is based on and inspired by the work shown in [Laptop](https://github.com/thoughtbot/laptop/blob/master/README.md), a version used by [The Associated Press](https://github.com/associatedpress/laptop) and a version used by [18F](https://github.com/18F/laptop).

### Public domain

thoughtbot's original work remains covered under an [MIT License](https://github.com/thoughtbot/laptop/blob/c997c4fb5a986b22d6c53214d8f219600a4561ee/LICENSE).

18F's work on this project is in the worldwide [public domain](LICENSE.md), as are contributions to our project. As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).
>
> All contributions to this project will be released under the CC0 dedication. By submitting a pull request, you are agreeing to comply with this waiver of copyright interest.
