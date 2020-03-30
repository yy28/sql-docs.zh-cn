1. 在所有群集节点上，打开 Pacemaker 防火墙端口。 若要使用 `firewalld` 打开这些端口，请运行以下命令：

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 如果防火墙没有内置高可用性配置，请打开 Pacemaker 的以下端口。
   >
   > * TCP：端口 2224、3121、21064
   > * UDP：端口 5405

1. 在所有节点上安装 Pacemaker 包。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

1. 为安装 Pacemaker 和 Corosync 包时创建的默认用户设置密码。 在所有节点上使用相同的密码。 

   ```bash
   sudo passwd hacluster
   ```

1. 若要在重启后允许节点重新加入群集，请启用并启动 `pcsd` 服务和 Pacemaker。 在所有节点上运行以下命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

1. 创建群集。 若要创建群集，请运行以下命令：

   **RHEL 7** 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3> 
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```

   **RHEL 8**

   对于 RHEL 8，需要单独对节点进行身份验证。 出现系统提示时，请手动输入 hacluster 的用户名和密码。

   ```bash
   sudo pcs host auth <node1> <node2> <node3>
   sudo pcs cluster setup <clusterName> <node1> <node2> <node3>
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >如果以前已在相同节点上配置了群集，则需要在运行 `--force` 时使用“`pcs cluster setup`”选项。 此选项等同于运行 `pcs cluster destroy`。 若要重新启用 pacemaker，请运行 `sudo systemctl enable pacemaker`。

1. 为 SQL Server 安装 SQL Server 资源代理。 在所有节点上运行以下命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```
