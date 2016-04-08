## これは何

Windowsは残念ながらAnsibleの実行ホストになれません。

http://docs.ansible.com/ansible/intro_windows.html#reminder-you-must-have-a-linux-control-machine

> Note running Ansible from a Windows control machine is NOT a goal of the project. Refrain from asking for this feature, as it limits what technologies, features, and code we can use in the main project in the future. A Linux control machine will be required to manage Windows hosts.
>
> Cygwin is not supported, so please do not ask questions about Ansible running from Cygwin.

WindowsマシンでもAnsibleが使いたい人はどうすれば？
Vagrantで仮想Linuxマシンを作ってそこにAnsibleを入れるのも手ですが、Dockerがあるじゃないですか、というサンプルです。

## 使い方

```
docker-compose run ansible
```

でCentOS7のbashが立ち上がる。

そして起動したコンテナのbashで、

```shell-session
[root@b153406376b5 playbook]# ansible-playbook -i hosts/dev site.yml

PLAY ***************************************************************************

TASK [setup] *******************************************************************
ok: [52.193.84.157]

TASK [hoge : hogehoge] *********************************************************
ok: [52.193.84.157]

TASK [hoge : debug] ************************************************************
ok: [52.193.84.157] => {
    "msg": " Amazon "
}

PLAY RECAP *********************************************************************
52.193.84.157              : ok=3    changed=0    unreachable=0    failed=0   
```

## 注意事項

* `playbook/hosts/dev`に書かれているIPは適当なEC2インスタンスのものなので接続先はなにか適当に用意してください
* ホストの`~/.ssh/docker-sample.pem`に上記接続先のSSH秘密鍵を置いてください（docker-compose.ymlの中を見てね)
