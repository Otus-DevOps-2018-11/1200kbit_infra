# 1200kbit_infra
1200kbit Infra repository
###ДЗ Cloud-Bastion

1. Способ подключения по ssh к внутреннему хосту в одну комнаду:
`ssh -o ProxyCommand='ssh -W %h:%p 1200kbit@35.210.101.122' 1200kbit@10.132.0.3`
2. Создаем файл ~/.ssh/config с описание хостов, пользователей и команд:
```
Host bastion
hostname 35.210.101.122
user 1200kbit

Host someinternalhost
hostname 10.132.0.3
user 1200kbit
proxycommand ssh bastion -W %h:%p
```
Теперь к внутреннему хосту можно подключиться командой:
`ssh someinternalhost`
При этом на someinternalhost видим, что наша ssh-сессия открыта с bastionhost:
```
1200kbit@someinternalhost:~$ w
 10:33:35 up  1:08,  1 user,  load average: 0.04, 0.01, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
1200kbit pts/0    10.132.0.2       10:32    0.00s  0.04s  0.00s w
```
