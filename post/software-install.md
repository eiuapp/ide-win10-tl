
软件安装次序

windows 下安装 

1. winrar
6. 百度网盘 
1. shadowsocks
2. chrome
8. git for windows
3. qq, wechat
5. 腾讯安全管家，及其下的软件管家中安装
    - notepad
    - vs code
9. emacs, spacemacs
10. wsl
5. runz

wsl 下安装

11. zsh
6. anaconda2, anaconda3
6. nvm, nodejs
9. gitbook
7. gvm, golang

## env ##

- os: win10
    - username: a
- wsl: ubuntu16.04
    - username: u

## step ##

## win10 ##

#### winrar ####

#### 百度网盘 ####

#### shadowsocks ####

去 github.com 中搜索 shadowsocks 并对应下载

如果您有在百度网盘中，则先下载使用百度网盘

#### chrome ####

依赖于 shadowsocks 外网，登录chrome帐户

#### qq, wechat ####

#### 腾讯电脑管家，及其下的软件管家 ####

#### 软件管家中安装软件 ####

- notepad
- vs code
- Beyond Compare


#### git for windows ####

安装后，就带有 curl

#### 迅雷 ####

https://www.xunlei.com/

#### virtualbox ####
#### vagrant ####
##### windows下切换vagrant_home目录 #####

https://eiuapp.github.io/vagrant-handbook/docs/change-vagrant_home-directory-windows.html

##### 搜索 box #####

https://app.vagrantup.com/boxes/search




#### xshell ####



## wsl ##

#### 修改 镜像源 

https://blog.csdn.net/china_jeffery/article/details/79715799

```
sudo cp /etc/apt/sources.list /etc/apt/sources.list_backup
sudo vi /etc/apt/sources.list
sudo apt-get update
```



#### 把默认用户的HOME修改成 C:\Users\Username ####

[ubuntu下修改用户的默认目录](https://blog.csdn.net/mifan88/article/details/7583016)（配置文件 /etc/passwd 中）

```
u@DESKTOP-APB1HCJ:~$ cd
u@DESKTOP-APB1HCJ:~$ pwd
/mnt/c/Users/a
u@DESKTOP-APB1HCJ:~$
```

#### 把个人 dotfiles 配置放入 ####

#### 生成新的 公私秘钥 ####

cd ~

#### .ssh 文件权限 配置 ####

如果不配置，会是

```
u@DESKTOP-APB1HCJ:~$ ls -l ~/.ssh/
total 8
-rwxrwxrwx 1 u u 1823 Apr 11 15:52 id_rsa
-rwxrwxrwx 1 u u  399 Apr 11 15:52 id_rsa.pub
-rwxrwxrwx 1 u u 2184 Apr 12 14:02 known_hosts
u@DESKTOP-APB1HCJ:~$
```

此时，即使你把这个公钥放入了github中的ssh_keys中，也会报下面错误。

```
u@DESKTOP-APB1HCJ:~$ git clone git@github.com:eiuapp/tl-lvchuang-java-sql.git
Cloning into 'tl-lvchuang-java-sql'...
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0777 for '/mnt/c/Users/a/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/mnt/c/Users/a/.ssh/id_rsa": bad permissions
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
u@DESKTOP-APB1HCJ:~$
```

总共要走2步:

- WSL开启chmod功能
- 解决 id_rsa 权限不够

##### WSL开启chmod功能 #####

- https://blog.pupt.net/wsl-enable-chmod.html
- https://blog.csdn.net/c13232906050/article/details/85274433

使用WSL终端SSH登录VPS的时候报错说私钥权限太宽松，执行chmod 600 ~/.ssh不管用。

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
WARNING: UNPROTECTED PRIVATE KEY FILE! 
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
Permissions 0777 for '~/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored. Load key "~/.ssh/id_rsa": bad permissions
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
```

上网搜索了一下，发现WSL默认不开启该功能。
```
vim /etc/wsl.conf
```
加入以下内容并保存，重启WSL就可以使用chmod命令了

```
[automount]
options = "metadata"
```
关闭所有bash，重新打开即可

##### 解决 id_rsa 权限不够 #####


解决方案 

```
chmod 755 ~/.ssh/ 
chmod 600 ~/.ssh/id_rsa ~/.ssh/id_rsa.pub 
chmod 644 ~/.ssh/known_hosts
```

参考：

- http://www.cnblogs.com/jacker1979/p/4547472.html


#### zsh ####

https://www.jianshu.com/p/9a5c4cb0452d

依赖于 curl

```
sudo apt install zsh -y
zsh --version
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

因为我自己的 dotfiles 配置，已经设置好了 .zshrc 文件，所以，这时的安装会覆盖我自己的 .zshrc 文件，所以，还原一下。

```
git status
cp .zshrc .zshrc.origin.bak
git checkout -- .zshrc
git status
```






## windows ##

#### cmder ####

##### 设置默认启动shell 为 wsl-shell #####

Startup/Tasks 下设置 

##### 设置 wsl-shell 的默认启动目录 #####

[ubuntu下修改用户的默认目录](https://blog.csdn.net/mifan88/article/details/7583016)（配置文件 /etc/passwd 中）

#### vscode ####

已通过 软件管家 安装

##### 配置所有文本，以 LF 作为行尾结束符 #####

`File/Preferences/Settings` 搜索 `CRLF` ，选择 `User Settings/Text Editor/Files: Eol` 替换成 `LF` 


##### 配置 wsl 作为 Terminal #####

参考：https://www.v2ex.com/t/461903

`File/Preferences/Settings` 搜索 `shell` ，选择 `User Settings/` 找到 `Terminal › Integrated › Shell: Windows`

把框中的

```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe 
```

修改成

```
C:\Windows\System32\wsl.exe
```

验证：

`View/Terminal` 打开即可。


#### anaconda2, anaconda3 ####

使用 清华镜像 下载

安装 anaconda3 和 anaconda2 时，一路默认设置，不要修改

#### emacs, spacemacs ####

https://eiuapp.github.io/post/emacs-install-with-win10/

https://eiuapp.github.io/post/spacemacs-install-with-win10/

安装完成后，会自动安装了一个python

```
C:\Users\a>where python
C:\Program Files\soft\emacs-26.1-x86_64\bin\python.exe

C:\Users\a>
```

##### snippets #####

```bash
git submodule update --init --recursive
```

#### runz ####

#### github cli ####

https://desktop.github.com/






## wsl ##

#### docker ####

##### install

https://docs.docker.com/install/linux/docker-ce/ubuntu/


##### 如何使用Docker加速器

针对Docker客户端版本大于1.10的用户
您可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器：

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{  
    "registry-mirrors": ["https://ce0d6wdn2yph.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```


##### 用户加入docker组

```bash
DESKTOP-APB1HCJ% echo $USER
DESKTOP-APB1HCJ% sudo usermod -aG docker $USER
```

##### 连接到其它机器上的 docker daemon

前置条件，有其它机器上，有开启 docker daemon 服务提供成服务，供外部机器使用。
所以，这一步，最好在 完成安装 virtualbox, vagrant 之后。

```bash
DESKTOP-APB1HCJ% echo "export DOCKER_HOST=tcp://192.168.168.164:2376" >> ~/.bashrc && source ~/.bashrc
DESKTOP-APB1HCJ% echo "export DOCKER_HOST=tcp://192.168.168.164:2376" >> ~/.zshrc && source ~/.zshrc
DESKTOP-APB1HCJ% docker ps
DESKTOP-APB1HCJ% sudo docker run hello-world
```



#### python2

```
sudo apt install python-minimal -y
```

#### pip

#### anaconda2, anaconda3 ####

##### 依赖 

会依赖于  ，如果没有安装，则会报下面错误：

```
[/mnt/c/Users/a/anaconda2] >>> /mnt/c/Users/a/anaconda2wslubuntu16/
PREFIX=/mnt/c/Users/a/anaconda2wslubuntu16
installing: python-2.7.16-h9bab390_0 ...
Python 2.7.16 :: Anaconda, Inc.
installing: conda-env-2.6.0-1 ...
installing: blas-1.0-mkl ...
installing: ca-certificates-2019.1.23-0 ...
installing: intel-openmp-2019.3-199 ...
installing: libgcc-ng-8.2.0-hdf63c60_1 ...
installing: libgfortran-ng-7.3.0-hdf63c60_0 ...
installing: libstdcxx-ng-8.2.0-hdf63c60_1 ...
installing: bzip2-1.0.6-h14c3975_5 ...
installing: expat-2.2.6-he6710b0_0 ...
installing: fribidi-1.0.5-h7b6447c_0 ...
installing: gmp-6.1.2-h6c8ec71_1 ...
installing: graphite2-1.3.13-h23475e2_0 ...
installing: icu-58.2-h9c2bf20_1 ...
installing: jbig-2.1-hdba287a_0 ...
installing: jpeg-9b-h024ee3a_2 ...
installing: libffi-3.2.1-hd88cf55_4 ...
installing: liblief-0.9.0-h7725739_2 ...
installing: libsodium-1.0.16-h1bed415_0 ...
installing: libtool-2.4.6-h7b6447c_5 ...
installing: libuuid-1.0.3-h1bed415_2 ...
installing: libxcb-1.13-h1bed415_1 ...
installing: lz4-c-1.8.1.2-h14c3975_0 ...
installing: lzo-2.10-h49e0be7_2 ...
installing: mkl-2019.3-199 ...
installing: ncurses-6.1-he6710b0_1 ...
Traceback (most recent call last):
  File "/mnt/c/Users/a/anaconda2wslubuntu16/pkgs/.install.py", line 599, in <module>
    main()
  File "/mnt/c/Users/a/anaconda2wslubuntu16/pkgs/.install.py", line 581, in main
    link_dist(opts.link_dist)
  File "/mnt/c/Users/a/anaconda2wslubuntu16/pkgs/.install.py", line 456, in link_dist
    link(prefix, dist, linktype)
  File "/mnt/c/Users/a/anaconda2wslubuntu16/pkgs/.install.py", line 345, in link
    raise Exception("dst exists: %r" % dst)
Exception: dst exists: '/mnt/c/Users/a/anaconda2wslubuntu16/share/terminfo/e/eterm'
➜  Downloads git:(master) ✗
```

<!-- 使用 清华镜像 下载 -->

<!-- 安装 anaconda3 和 anaconda2 时，一路默认设置，不要修改 -->

#### nvm, nodejs ####

依赖于 curl, zsh

https://eiuapp.github.io/post/nodejs-install/

#### gitbook ####

依赖于 nodejs

```bash
npm install -g gitbook gitbook-cli 
```

#### gvm, golang ####

#### rvm, ruby ####
##### install rvm #####

```bash
which gpg2
sudo apt-get install gnupg2 -y
gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
curl -sSL https://get.rvm.io | bash -s stable --rails
# 或者 curl -L https://get.rvm.io | bash -s stable
```
 