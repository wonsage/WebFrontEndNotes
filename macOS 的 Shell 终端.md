从 macOS 10.15 Catalina 开始，终端默认为 zsh，其他的还有 bash、dash、tsh等。从bash进入zsh只需要输入：zsh即可，相反也是一样。
zsh 的用户配置文件 `~/.zshrc`，系统配置文件 `/etc/zshrc`
阅读链接：[Where the .zshrc File is Located on Mac (osxdaily.com)](https://osxdaily.com/2021/11/18/where-the-zshrc-file-is-located-on-mac/)
bash 的用户配置文件：
- `~/.bash_profile`：每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件。
- `~/.bashrc`: 该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,该该文件被读取。
bash的系统配置文件：
- `/etc/profile`: 此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行.并从/etc/profile.d目录的配置文件中搜集shell的设置。
- `/etc/bashrc`:  为每一个运行bash shell的用户执行此文件.当bash shell被打开时,该文件被读取。

编辑环境变量文件：
0. 如果没有文件，先创建文件 `touch ~/.zshrc`
1. 打开、编辑、保存 `open -e ~/.zshrc` | `vi .zshrc` | `code .zshrc`
2. 应用修改后的环境变量 `source ~/.zshrc`

