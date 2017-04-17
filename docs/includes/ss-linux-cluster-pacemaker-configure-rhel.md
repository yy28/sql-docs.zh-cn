
3. 在两个群集节点上，打开 Pacemaker 防火墙端口。 若要使用 `firewalld` 打开这些端口，请运行以下命令：

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

   

2. 为安装 Pacemaker 和 Corosync 包时创建的默认用户设置密码。 在两个节点上使用相同的密码。 

   ```bash
   sudo passwd hacluster
   ```

   

3. 启用并启动 `pcsd` 服务和 Pacemaker。 这样，节点将可以在重新启动后重新加入群集。 在两个节点上运行以下命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 创建群集。 若要创建群集，请运行以下命令：

   ```bash
   sudo pcs cluster auth <nodeName1> <nodeName2…> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <nodeName1> <nodeName2…> 
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >如果以前已在相同节点上配置了群集，则需要在运行“pcs cluster setup”时使用“--force”选项。 请注意，这相当于运行“pcs cluster destroy”，需要使用“sudo systemctl enable pacemaker”重新启用 pacemaker 服务。

5. 为 SQL Server 安装 SQL Server 资源代理。 在两个节点上运行以下命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```
