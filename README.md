# vagrant-centos65-x86_64-gitolite

vagrant recipe for installing gitolite server

## Installation

```
$ git clone https://github.com/mattn/vagrant-centos65-x86_64-gitolite
$ cd vagrant-centos65-x86_64-gitolite
$ mkdir .vagrant
$ ssh-keygen -t rsa # generate if key doesn't already exist
$ cp /path/to/your/ssh/public/key/id_rsa.pub .vagrant/admin.pub
$ vagrant up
```

*NOTE*: filename of `admin.pub` should be `<username>.pub` for administrator.

## Create gitolite repository

*NOTE*: At the first, remove line begining with `[127.0.0.1]:2222` in `~/.ssh/known_hosts`.

```
$ git clone ssh://gitolite@127.0.0.1:2222/gitolite-admin.git 
$ cd gitolite-admin
$ vi conf/gitolite.conf
```

Append two lines for new repository. See gitolite's [README](https://github.com/sitaramc/gitolite#readme) for description.

```
repo    gitolite-admin
        RW+     =   admin

repo    testing
        RW+     =   @all

repo    example
        RW+     =   @all
```

```
$ git commit -am "Add example" && git push
# git repos are in /var/lib/gitolite/repositories/
```
## Use the repository

```
$ git clone ssh://gitolite@127.0.0.1:2222/example.git
$ cd example
$ echo ﾊｧﾊｧ > poem.txt
$ git add poem.txt && git commit -m 'First ﾊｧﾊｧ'
$ git push
```

Open http://127.0.0.1:4567/git in your browser.

![](http://go-gyazo.appspot.com/71c643d3e5834879.png)

## 

## Author

Yasuhiro Matsumoto (a.k.a mattn)
