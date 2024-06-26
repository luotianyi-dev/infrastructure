# Tianyi Network 基础设施

此项目基于 IaC (Infrastructure as Code) 思想，使用 ansible、docker-compose、octodns 等工具，旨在实现自动化的技术设施复现与水平扩展。

## Ansible 部署和维护项目

### 先决条件

服务端先决条件：
 - 操作系统：Arch Linux

客户端先决条件：
 - **安装 ansible**：您需要安装 ansible 及相关社区模块。推荐您使用 `pipx` 安装。
   ```bash
   pipx install ansible
   ansible-galaxy collection install community.general
   ansible-galaxy collection install community.docker
   ansible-galaxy collection install community.mysql
   ansible-galaxy collection install community.crypto
   ```
 - 您已在 `~/.ssh/config` 中配置了相关 hostname，并确保可以通过 SSH 连接到服务器，并具有 root 权限。配置示例如下：
   ```
   Host haru
       HostName <ip-addr>
       User root
   Host monologue
       HostName <ip-addr>
       User root
   Host starlight
       HostName <ip-addr>
       User root
   ```


### 服务器初始化部署

**Web 服务器**

```bash
cd ansible
ansible-playbook playbooks/setup_web.yml
```

**DNS 权威服务器**

```bash
cd ansible
ansible-playbook playbooks/setup_ns.yml
```

**配置所有服务器的 Wireguard 互联**

```bash
cd ansible
ansible-playbook playbooks/wireguard.yml
```

**配置 Web 服务器的 DeployKit 静态网站部署**
在执行此步骤前，请确保您已经使用 acme.sh 完成了证书的申请。
```bash
cd ansible
ansible-playbook playbooks/deploykit.yml
```
