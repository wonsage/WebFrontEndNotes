手动安装
通常将JDK目录（内含一个content文件夹）放在系统根目录的`/Library/Java/JavaVirtualMachines/`下，在`~/.zshrc`中指定JAVA_HOME为`/Library/Java/JavaVirtualMachines/{YOUR_SDK_DIRNAME}/content/Home`
修改shell config后，需要`source ~/.zshrc`以应用更改。
然后，使用命令`echo $JAVA_HOME`可以看到设置的路径，或者`env`可以看到所有的path。

Homebrew 安装
无需在Shell中手动配置path
