<!--
title:   【AlmaLinux】 SSHログイン時の "Activate the web console with: ~" を削除する
tags:    AlmaLinux,RHEL,cockpit
id:      fdb97af4bdb8575f6fd0
private: false
-->
CentOS系のLinuxディストリビューション「AlmaLinux」では、Webベースの管理コンソールサービス「cockpit.socket」が標準インストールされているため、SSHログイン時に以下のメッセージが出力される場合がある。

```
Activate the web console with: systemctl enable --now cockpit.socket
```

この表示は鬱陶しいので削除する方法を以下に記載する。

## cockpit.socket 削除方法

```shell
sudo systemctl stop cockpit
sudo dnf remove -y cockpit
sudo rpm -e cockpit-storaged
sudo rpm -e cockpit-system
sudo rpm -e cockpit-podman
sudo rpm -e cockpit-packagekit
sudo rpm -e cockpit-bridge
sudo rpm -e cockpit-ws
sudo rm -Rf /run/cockpit
sudo rm -Rf /etc/cockpit
sudo rm -Rf /usr/share/cockpit
```

## 参考

https://qiita.com/CloudRemix/items/8b318c19e001d5a9b40d


以上！