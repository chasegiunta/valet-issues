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
