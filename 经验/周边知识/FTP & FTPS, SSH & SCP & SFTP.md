FTP 文件管理协议
FTPS：FTP over SSL

SSH (Secure Shell): 一个守护进程，服务端的进程名为sshd，监听客户端22端口的请求。包括OpenSSH和OpenSSL两部分。
SCP和SFTP都基于SSH，SCP用以主机间通过网络快速传输文件。
SCP传输速度快，不需要等待数据包确认。
SFTP更强大，提供断点续传等功能。