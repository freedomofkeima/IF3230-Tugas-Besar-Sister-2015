# LoliHorizon - Tracker

By: Assistants of IF3230 - Parallel and Distributed Systems

## Development Environment

- Linux x86_64

- Go Language 1.4.2

## Requirements

** Environment Set **

Set the following lines to ```/etc/profile```:

    export PATH=$PATH:/usr/local/go/bin

    export GOPATH=$HOME/go

** Download MySQL Driver **

    $go get github.com/go-sql-driver/mysql

** For 1st MySQL use **

    $sudo chmod -R 755 /var/lib/mysql/

    $sudo mkdir /var/run/mysqld

    $sudo touch /var/run/mysqld/mysqld.sock

    $sudo chown -R mysql /var/run/mysqld/

    $sudo /etc/init.d/mysql start


## How to Run

For maintaining our process to keep running in the presence of failure, we'll use Monit 5.5 with the following configuration in ```etc/monit.conf```:

```
### Monitor Sister Tracker
check process sistertracker with pidfile /home/path-to-file/run.pid
  start program = "/bin/bash -c 'cd /home/path-to-file; nohup /path-to-go/bin/go run main.go >> my.log 2>&1 & echo $! > run.pid'" with timeout 5 seconds
  stop program ="/bin/kill -9 `cat /home/path-to-file/run.pid`"
```

After that, you can simply use ```service monit start``` to start Monit.


Last Updated: April 24, 2015
