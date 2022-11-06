# Ansible_k8s_install

# 使い方メモ

## 環境前提

- fedora36 を 4 OS 分用意
- ansible ユーザーを作成、 sudoers に設定
- SELinux は事前に disabled に変更（別に ansible で実施してもよい )
- IPv6 無効化 (別に ansible で実施してもよい )

## ansible 実行方法

0. ansible-vault encrypt-string で ansible ユーザーのパスワードを暗号化し、group_vars/all.yml 内に格納する。（ all.yml.sample あり )

1. roles/08_k8s_mkcluster/vars/main/k8s_networks.yml 内の `pod_network_cidr` 変数について、 k8s の cluster で利用する NW アドレスに変更する（必要時）

2. roles/09_calico/tasks/install_calico.yml 内の `edit calico yaml file` 部分で、 replace の NW アドレスを 上記 pod_network_cidr の内部に収まる NW アドレスに変更する

3. `ansible-playbook c1_all.yml` 実行

