# Installation

For the most part, follow: 
https://medium.com/@jalendport/running-craft-cms-3-on-laravel-valet-6df61e5193fd

Couple notes:
 - If the incorrect PHP version (`usr/bin/php` - default Mac php) is showing when running `which php`, restart terminal. If it's _still_ not showing the correct (`usr/local/bin/php`), run `brew link --force php@7.1` (or whichever php version you've installed)
 
- Running `pecl` should also be recognized (this is used for installing php extensions)

- For imagemagick (imagick) to be installed & recognized:
```
brew install autoconf pkg-config imagemagick
mkdir /usr/local/lib/php/pecl  # If this dir doesn't exist it will cause pecl install to fail
pecl install imagick
brew services restart php@7.1  # Or valet restart
```
 
- If valet isn't found when running `valet install`, restart your terminal. If it's _still_ not found, replace the composer executable line with `export PATH="$PATH:$HOME/.composer/vendor/bin"` in your .bashrc, or .zshrc file (`~` parsing problems, it seems. `$HOME` ftw).

# Initial Configuration

Right away, you might want to dig into `/usr/local/etc/php/[versionNumber]/conf.d/php-memory-limits.ini` and increase some limits like `memory_limit` to something above the default `128M`. It's unclear why memory limits is managed in a separate file, but for other settings like `max_input_vars` for those projects with extraordinary amounts of fields in matrix content builders, look in `/usr/local/etc/php/[versionNumber]/php.ini`

Settings to search for:

- `memory_limit` ( exists in `conf.d/php-memory-limits.ini` & `php.ini` )
- `upload_max_filesize` ( exists in `conf.d/php-memory-limits.ini` & `php.ini` )
- `max_input_vars`
- `max_execution_time`

You'll want to `valet restart` after changing these settings.

# valet-issues

#### Can't read dir of '/usr/local/etc/my.cnf.d' (Errcode: 2 "No such file or directory")

`mkdir /usr/local/etc/my.cnf.d`

(https://github.com/Homebrew/legacy-homebrew/issues/31760)


#### ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)

1. If you are able to see "mariadb stopped" when you run below command;

`brew services list`

2. and if you are able to start mariadb with below command;

`mysql server start`
then, adding mysql to services will fix your problem. With this method, mysql will start as service when your operating system started. To do so you can run below command;

`brew services start mariadb`

After that, you can restart your system and try connecting to mariadb.
(https://stackoverflow.com/a/34709790/4565664)
