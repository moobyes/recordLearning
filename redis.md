

redis-server redis的启动

redis-cli shutdown  或者 kill redis进程的pid  关闭redis

可以用终端命令简单的处理掉，并且防止 DS_Store 文件的再生。

　　我们需要打开终端窗口，并输入删除命令：sudo find / -name ".DS_Store" -depth -exec rm {} \;

　　按下回车键盘之后，终端会提示用户名和密码，直接输入密码再按回车即可。

　　删除后继续在终端输入：defaults write com.apple.desktopservices DSDontWriteNetworkStores true



