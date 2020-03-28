# python3 相关总结

## 没发现命令，配置

```shell
ln -s /usr/local/Cellar/python/3.7.7/bin/python3 /usr/local/bin/python3
```

### 具体操作
#### 一、打开以下目录, 版本号有可能不同
```shell
cd /usr/local/Cellar/python/3.7.7/bin
```

#### 二、 查看当前目录的内容
```shell
ls
```

#### 三、建立软连接
1. python3的软连接
```shell
# 需要软连接到 /usr/local/bin 目录下
ln -s /usr/local/Cellar/python/3.7.7/bin/python3 /usr/local/bin/python3
```
2. pip3的软连接
```shell
# 下面是 pip3 的软连接,没有需求,可以忽略
ln -s /usr/local/Cellar/python/3.7.7/bin/pip3.7 /usr/local/bin/pip3
```

###  软连接命令说明:
> ln [-bfis] existing-file-list(source) new-link
-b     如果需要创建的目标连接已存在相同文件名,则备份
-f     强制创建目标链接
-i     覆盖相同文件名时提示
-s     创建符号连接
>

## Mac 下通过Homebrew 安装Anaconda

```shell
# 查找anconda的位置
brew search anaconda

# 安装，中间需要输入电脑密码
brew cask install anaconda

# 配置环境变量
echo 'export PATH=/usr/local/anaconda3/bin:$PATH' >> ~/.bash_profile
source ~/.bash_profile  

# 测试是否安装成功
conda -V
```
