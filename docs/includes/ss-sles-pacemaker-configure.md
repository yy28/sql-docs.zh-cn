1. **在两个群集节点上，创建一个文件来存储用于 Pacemaker 登录的 SQL Server 用户名和密码**。 以下命令创建并填充此文件：

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **所有群集节点都必须能够通过 SSH 相互访问**。 hb_report 或 crm_report（用于故障排除）和 Hawk 的历史记录浏览器等工具需要在节点之间进行无密码的 SSH 访问，否则它们只能收集当前节点的数据。 如果使用非标准 SSH 端口，请使用 -X 选项（请参见手册页）。 例如，如果 SSH 端口为 3479，请使用以下命令调用 hb_report：

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    有关详细信息，请参阅 [SUSE 文档中的系统要求和建议](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)。

3. **安装高可用性扩展**。 若要安装该扩展，请按照以下 SUSE 主题中的步骤操作：
    
    [安装和设置快速入门](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)

4. **为 SQL Server 安装 FCI 资源代理**。 在两个节点上运行以下命令：

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **自动设置第一个节点**。 下一步是通过配置第一个节点（SLES1）设置一个正在运行的单节点群集。 按照 SUSE 主题中[设置第一个节点](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)的说明进行操作。

    完成后，使用 `crm status` 检查群集状态：
    ```bash
    crm status
    ```

    它应显示一个节点（SLES1）已配置。

6. **将节点添加到现有群集**。 接下来将 SLES2 节点加入群集。 按照 SUSE 主题中[添加第二个节点](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node)的说明进行操作。
    
    完成后，使用 **crm status** 检查群集状态。 如果已成功添加第二个节点，则输出将如下所示：
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** 是最初单节点群集安装期间配置的虚拟 IP 群集资源。

7.  **删除过程**。 如果需要从群集中删除节点，请使用 **ha-cluster-remove** 启动脚本。 有关详细信息，请参阅[启动脚本概述](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap)。  

