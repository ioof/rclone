supervisord -c /etc/supervisor/supervisord.conf

supervisorctl 是 supervisord的命令行客户端工具

supervisorctl status：查看所有进程的状态
supervisorctl stop es：停止es
supervisorctl start es：启动es
supervisorctl restart es: 重启es
supervisorctl update ：配置文件修改后可以使用该命令加载新的配置
supervisorctl reload: 重新启动配置中的所有程序
