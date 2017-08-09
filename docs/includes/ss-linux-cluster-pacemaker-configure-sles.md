2. 在所有群集节点上，创建一个文件来存储用于登录 Pacemaker 的 SQL Server 用户名和密码。 以下命令创建并填充此文件：

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
   sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. 在所有群集节点上，打开 Pacemaker 防火墙端口。 若要使用 `firewalld` 打开这些端口，请运行以下命令：

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 如果使用的是没有内置高可用性配置的其他防火墙，则需要打开以下端口，Pacemaker 才能与群集中的其他节点通信
   >
   > * TCP：端口 2224、3121、21064
   > * UDP：端口 5405

1. 在每个节点上安装 Pacemaker 包。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. 为安装 Pacemaker 和 Corosync 包时创建的默认用户设置密码。 在所有节点上使用相同的密码。 

   ```bash
   sudo passwd hacluster
   ```

   

3. 启用并启动 `pcsd` 服务和 Pacemaker。 这样，节点将可以在重新启动后重新加入群集。 在所有节点上运行以下命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 为 SQL Server 安装 FCI 资源代理。 在所有节点上运行以下命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```
