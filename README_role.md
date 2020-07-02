# Ansible Role: Zabbix40-Agent_setup for RHEL6/RHEL7

# Trademarks
-----------
* Linuxは、Linus Torvalds氏の米国およびその他の国における登録商標または商標です。
* RedHat、RHEL、CentOSは、Red Hat, Inc.の米国およびその他の国における登録商標または商標です。
* Windows、PowerShellは、Microsoft Corporation の米国およびその他の国における登録商標または商標です。
* Ansibleは、Red Hat, Inc.の米国およびその他の国における登録商標または商標です。
* pythonは、Python Software Foundationの登録商標または商標です。
* Zabbixは、ラトビア共和国にあるZabbix LLCの商標です。
* Oracleは、Oracle International Corporation の米国およびその他の国における登録商標または商標です。
* NECは、日本電気株式会社の登録商標または商標です。
* その他、本ロールのコード、ファイルに記載されている会社名および製品名は、各社の登録商標または商標です。

## Description
本Roleは統合監視ソフトウェア"Zabbix"のエージェント"Zabbix Agent"のセットアップを行います。<br/>
対象バージョンは以下のバージョンです。
- Zabbix 4.0

以下のファイルを設定します。
- /etc/zabbix/zabbix_agentd.conf
- /etc/logrotate.d/zabbix-agent

## Supports
- 管理マシン(Ansibleサーバ)
  - Linux系OS（RHEL/CentOS）
  - Ansible バージョン2.5 以上 (動作確認済み：2.5、2.6)
  - Python バージョン2.6 または 2.7

- 管理対象マシン(インストール対象マシン)
  - RHEL6 または RHEL7
  - Python 2.6以上  

## Requirements
- 管理マシン(Ansibleサーバ)
  - 管理対象マシンへroot権限でSSH接続できること
- 管理対象マシン(インストール対象マシン)
  - Zabbix Agentがインストールされていること
  - SELinuxが無効に設定されていること
  - iptables, firewalldが適切に設定されていること

## Role Variables
### Mandatory variables

実行時には以下の変数を必ず指定します。

- Zabbix Agent 設定ファイル 「/etc/zabbix/zabbix_agentd.conf」
  - ''VAR_Zabbix40AG_Server''：Server (string)
  - ''VAR_Zabbix40AG_ServerActive'': ServerActive (string)

### Optional variables

以下の変数は任意で指定します。

- Zabbix Agent サービス起動設定
  - ''VAR_Zabbix40AG_chkconfig'': サーバ起動時のサービス起動設定 (on|off, default: "")
  - ''VAR_Zabbix40AG_start'': 設定完了時にサービスを再起動するか (string: default:"")  
    - "yes"を指定した場合のみサービスを再起動する


- Zabbix Agent 設定ファイル 「/etc/zabbix/zabbix_agentd.conf」
  - ''VAR_Zabbix40AG_Hostname'': Hosname (string, default: "{{ ansible_hostname }}")   
      - デフォルト値は、Ansible設定のホスト名が設定される
  - ''VAR_Zabbix40AG_LogType'': LogType (string, default: "")
  - ''VAR_Zabbix40AG_LogFile'': LogFile (string, default: /var/log/zabbix/zabbix_agentd.log)
  - ''VAR_Zabbix40AG_LogFileSize'': LogFileSize (string, default: 0)
  - ''VAR_Zabbix40AG_SourceIP'': SourceIP (string, default: "")
  - ''VAR_Zabbix40AG_DebugLevel'': DebugLevel (string, default: "")
  - ''VAR_Zabbix40AG_EnableRemoteCommands'': EnableRemoteCommands (string, default: "")
  - ''VAR_Zabbix40AG_LogRemoteCommands'': LogRemoteCommands (string, default: "")
  - ''VAR_Zabbix40AG_ListenPort'': ListenPort (string, default: "")
  - ''VAR_Zabbix40AG_ListenIP'': ListenIP (string, default: "")
  - ''VAR_Zabbix40AG_StartAgents'': StartAgents (string, default: "")
  - ''VAR_Zabbix40AG_HostnameItem'': HostnameItem (string, default: "")
  - ''VAR_Zabbix40AG_HostMetadata'': HostMetadata (string, default: "")
  - ''VAR_Zabbix40AG_HostMetadataItem'': HostMetadataItem (string, default: "")
  - ''VAR_Zabbix40AG_RefreshActiveChecks'': RefreshActiveChecks (string, default: "")
  - ''VAR_Zabbix40AG_BufferSend'': BufferSend (string, default: "")
  - ''VAR_Zabbix40AG_BufferSize'': BufferSize (string, default: "")
  - ''VAR_Zabbix40AG_MaxLinesPerSecond'': MaxLinesPerSecond (string, default: "")
  - ''VAR_Zabbix40AG_Alias'': Alias (array[], default: "")
      - 配列形式で設定可能
  - ''VAR_Zabbix40AG_Timeout'': Timeout (string, default: "")
  - ''VAR_Zabbix40AG_AllowRoot'': AllowRoot (string, default: "")
  - ''VAR_Zabbix40AG_User'': User (string, default: "")
  - ''VAR_Zabbix40AG_Include'': Include (array[], default: /etc/zabbix/zabbix_agentd.d/)
        - 配列形式で設定可能
  - ''VAR_Zabbix40AG_UnsafeUserParameters'': UnsafeUserParameters (string, default: "")
  - ''VAR_Zabbix40AG_UserParameter'': UserParameter (array[], default: "")
          - 配列形式で設定可能
  - ''VAR_Zabbix40AG_LoadModulePath'': LoadModulePath (string, default: "")
  - ''VAR_Zabbix40AG_LoadModule'': LoadModule (array[], default: "")
      - 配列形式で設定可能
  - ''VAR_Zabbix40AG_TLSConnect'': TLSConnect (uncrypted|psk|cert, default: "")
  - ''VAR_Zabbix40AG_TLSAccept'': TLSAccept (uncrypted|psk|cert, default: "")
  - ''VAR_Zabbix40AG_TLSCAFile'': TLSCAFile (string, default: "")
  - ''VAR_Zabbix40AG_TLSCRLFile'': TLSCRLFile (string, default: "")
  - ''VAR_Zabbix40AG_TLSServerCI'': TLSServerCertIssuer (string, default: "")
  - ''VAR_Zabbix40AG_TLSServerCS'': TLSServerCertSubject (string, default: "")
  - ''VAR_Zabbix40AG_TLSCertFile'': TLSCertFile (string, default: "")
  - ''VAR_Zabbix40AG_TLSKeyFile'': TLSKeyFile (string, default: "")
  - ''VAR_Zabbix40AG_TLSPSKId'': TLSPSKIdentity (string, default: "")
  - ''VAR_Zabbix40AG_TLSPSKFile'': TLSPSKFile (string, default: "")


- Zabbix Agentのログローテート設定ファイル 「/etc/logrotate.d/zabbix-agent」
  - ''VAR_Zabbix40AG_LogFile'': ログファイルパス名 (string, default: /var/log/zabbix/zabbix_agentd.log)
  - ''VAR_Zabbix40AG_RotateCount'': 世代数 (number, default: 12)
  - ''VAR_Zabbix40AG_RotateTiming'': 周期 (daily|weekly|monthly, default: weekly)

## Usage
1. 本Roleを用いたPlaybookを作成します。
2. 必須変数を指定します。
3. 任意変数を必要に応じて指定します。
4. Playbookを実行します。

## Example Playbook

インストールとすべての設定を行う場合は、提供した以下のRoleを"roles"ディレクトリに配置した上で、以下のようなPlaybookを作成してください。

- フォルダ構成
~~~
  - group_vars/
    ・ server1
    ・ server2
  - host_vars/
    ・ host1
    ・ host2
  - roles/
    ・ Zabbix40-Agent_install/
    ・ Zabbix40-Agent_regist/
    ・ Zabbix40-Agent_setup/
  - Zabbix40-Agent_install.yml
  - Zabbix40-Agent_regist.yml
  - Zabbix40-Agent_setup.yml
  - conf.yml
  - hosts
  - site.yml
~~~


- マスターPlaybookサンプル 「Zabbix40-Agent_setup.yml」
~~~
# Zabbix40-Agent_setup.yml
 - name: setup Zabbix40_Agent
   hosts: all
   gather_facts: yes
   become: yes
   tags:
    - setup
   roles:
     - Zabbix40-Agent_setup
~~~


## Running Playbook
- extra-vars を利用する場合の実行例
> ansible-playbook site.yml -k -i hosts --extra-vars="@conf.yml"

- group_vars を利用する場合の実行例  
group_vars で指定したグループ名が webserver1 の場合
> ansible-playbook site.yml -k -i hosts -l webserver1

- host_vars を利用する場合の実行例  
host_vars で指定したグループ名が server1 の場合
> ansible-playbook site.yml -k -i hosts -l server1

- 本Roleのみを実行する場合は、 --tags "setup" を付け加える
> ansible-playbook site.yml -k -i hosts --extra-vars="@conf.yml" --tags "setup"

# Copyright
Copyright (c) 2018 NEC Corporation

# Author Information
NEC Corporation
