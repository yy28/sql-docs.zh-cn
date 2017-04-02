---
title: "在 Azure 虚拟机上安装 SQL Server R 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# 在 Azure 虚拟机上安装 SQL Server R 服务
 
如果你部署 Azure 虚拟机包含 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，现在可以选择 R Services 作为一项功能时创建的 VM 要添加到的实例。 



+ [使用 SQL Server 2016 和 R Services 中创建新的 VM](#new)
+ [将 R Services 添加到现有虚拟机与 SQL Server 2016](#existing)

## <a name="a-namenewacreate-a-new-sql-server-2016-enterprise-virtual-machine-with-r-services-enabled"></a><a name="new"></a>启用 R 服务使用创建新的 SQL Server 2016 Enterprise 虚拟机

1. 在 Azure 门户中，单击虚拟机，然后单击新建。
2. 选择 SQL Server 2016 Enterprise Edition。
3. 配置服务器名称和帐户权限，并选择定价计划。
4. 在 VM 中的步骤 4 上安装向导，在 **SQL Server 设置**, ，找到 **R Services （高级分析）** 单击 **启用**。
5. 查看显示的验证和单击摘要 **确定**。
6. 虚拟机准备就绪后，连接到它，并打开 SQL Server Management Studio，这是预安装。 R Services 已准备好运行。 
7. 若要验证这一点，可以打开一个新查询窗口并运行以下命令，使用 R 来生成从 1 到 10 的数字序列的简单语句。
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. 如果你将连接到该实例从远程数据科学客户端，完成 [其他步骤](#additional-steps) 根据需要。


## <a name="additional-steps"></a>其他步骤  

可能需要执行一些其他步骤才能使用 R 服务，如果希望远程客户端访问服务器作为远程 SQL Server 计算上下文。

### <a name="a-namefirewallaunblock-the-firewall"></a><a name="firewall"></a>取消阻止防火墙  
  
必须更改以确保可以访问虚拟机上的防火墙规则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 从远程数据科学客户端的实例。  否则，你可能不能使用的计算需要的上下文使用的虚拟机的工作区。 

默认情况下，Azure 虚拟机上的防火墙包括阻止网络本地 R 用户帐户访问的规则。  
  
若要从远程数据科学客户端启用对 R 服务的访问︰
1. 虚拟机上打开高级安全 Windows 防火墙。
2. 选择 **出站规则**
3. 禁用以下规则︰  
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`  
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>为远程客户端启用 ODBC 回调

如果你预计 R 客户端调用服务器将需要发出 ODBC 查询作为其 R 解决方案的一部分，你必须确保快速启动板可代表远程客户端的 ODBC 调用。 若要执行此操作，必须允许快速启动板用于登录到实例的 SQL 工作帐户。
有关详细信息，请参阅 [设置 SQL Server R 服务](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。 

### <a name="a-namenetworkaadd-network-protocols"></a><a name="network"></a>添加网络协议  
  
+ 启用命名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 客户端和服务器计算机之间的连接，以及对某些内部连接，请使用命名管道协议。 如果未启用命名管道，必须安装并启用它，这两个 Azure 虚拟机上，并连接到服务器的任何数据科学客户端上。  
  
+ 启用 TCP/IP

  TCP/IP 是必需的环回连接到 SQL Server R Services。 如果你收到以下错误，支持实例 DBNETLIB; 虚拟机上启用 TCP/IPSQL Server 不存在或访问被拒绝。

## <a name="how-to-disable-r-services-on-an-instance"></a>如何在实例上禁用 R Services

你还可以启用或禁用现有的虚拟机上的功能在任何时间。 

1. 打开虚拟机边栏选项卡
2. 单击 **设置**, ，然后选择 **SQL Server 配置**。


## <a name="a-nameexistingaadd-sql-server-r-services-to-an-existing-sql-server-2016-enterprise-virtual-machine"></a><a name="existing"></a>将 SQL Server R Services 添加到现有的 SQL Server 2016 Enterprise 虚拟机

如果你使用不包括 R Services 的 SQL Server 2016 中创建 Azure VM，你可以通过执行以下步骤添加该功能︰

1. 重新运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 设置并在上添加功能 **服务器配置** 向导页。
2. 启用外部脚本执行，并重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 有关详细信息，请参阅 [设置 SQL Server R 服务](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。
3. （可选）如果所需的远程脚本执行，请配置 R 工作人员帐户的数据库的访问。
   有关详细信息，请参阅 [设置 SQL Server R 服务](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。 
3. （可选）如果你想要允许来自远程数据科学客户端的 R 脚本执行，请修改 Azure 虚拟机上的防火墙规则。 有关详细信息，请参阅 [取消阻止防火墙](#firewall)。
4. 安装或启用所需的网络库。 有关详细信息，请参阅 [添加网络协议](#network)。

## <a name="see-also"></a>另请参阅
[设置 Sql Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)