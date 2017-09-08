---
title: "在 Azure 虚拟机上安装 SQL Server R Services | Microsoft Docs"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e673268b1f6b56890f22576d293135b2675ed4ab
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="installing-sql-server-r-services-on-an-azure-virtual-machine"></a>在 Azure 虚拟机上安装 SQL Server R Services
 
如果你部署 Azure 虚拟机包含[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，现在可以选择机器学习，作为一项功能时创建的 VM 要添加到的实例。

+ [创建包含 SQL Server 2016 和 R Services 的新 VM](#new)
+ [将 R Services 添加到包含 SQL Server 2016 的现有虚拟机](#existing)

## <a name="new"></a>创建启用 R Services 的新 SQL Server 2016 Enterprise 虚拟机

1. 在 Azure 门户中，单击虚拟机，然后单击新建。
2. 选择“SQL Server 2005 Enterprise Edition”。
3. 配置服务器名称和帐户权限，然后选择定价计划。
4. 执行 VM 安装向导中的步骤 4 时，请在“SQL Server 设置”中找到“R Services (高级分析)”，然后单击“启用”。
5. 查看用于验证的摘要，然后单击“确定”。
6. 虚拟机准备就绪后，请与它建立连接，然后打开预先安装的 SQL Server Management Studio。 R Services 已准备好运行。
7. 若要验证是否可运行，可以打开一个新的查询窗口，然后运行如下所示的简单语句（使用 R 生成从 1 到 10 的序列号）。
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. 若要从远程数据科学客户端连接到实例，请根据需要完成[附加步骤](#additional-steps)。


## <a name="additional-steps"></a>额外的步骤  

如果希望远程客户端访问服务器作为远程 SQL Server 计算上下文，则需要执行一些其他步骤。

### <a name="firewall"></a>取消阻止防火墙

默认情况下，Azure 虚拟机上的防火墙包含一项规则，该规则阻止本地 R 用户帐户的网络访问。

必须禁用此规则，以确保可以访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从远程数据科学客户端的实例。  否则，R 代码无法执行中使用虚拟机的工作区的计算上下文中，即使其他 R 代码使用正常的 SQL Server 计算上下文。

若要从远程数据科学客户端访问 R Services，请执行以下操作：

1. 在虚拟机上打开“高级安全 Windows 防火墙”。
2. 选择“出站规则”。
3. 禁用以下规则：
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>启用远程客户端的 ODBC 回调

如果预期调用服务器的 R 客户端需要发出 ODBC 查询作为其 R 解决方案的一部分，必须确保 Launchpad 能够代表远程客户端发出 ODBC 调用。 为此，必须允许 Launchpad 使用的 SQL 辅助角色帐户登录到实例。
有关详细信息，请参阅 [安装 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。

### <a name="network"></a>添加网络协议

+ 启用命名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 对客户端与服务器计算机之间的连接以及某些内部连接使用命名管道协议。 如果未启用命名管道，必须同时在 Azure 虚拟机以及连接到服务器的任何数据科学客户端上安装并启用命名管道。
  
+ 启用 TCP/IP

  与 SQL Server R Services 建立环回连接需要 TCP/IP。 如果你收到以下错误，虚拟机支持实例上启用 TCP/IP:

  "DBNETLIB;SQL Server 不存在或拒绝访问"

## <a name="how-to-disable-r-services-on-an-instance"></a>如何在实例上禁用 R Services

也可以随时在现有虚拟机上启用或禁用该功能。

1. 打开虚拟机边栏选项卡
2. 单击“设置”，然后选择“SQL Server 配置”。

## <a name="existing"></a>将 SQL Server R Services 添加到现有的 SQL Server 2016 Enterprise 虚拟机

如果你创建 Azure 虚拟机未包括 R Services，你可以通过执行以下步骤添加该功能：

1. 重新运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序，在向导的“服务器配置”页上添加该功能。
2. 启用外部脚本执行并重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 有关详细信息，请参阅 [安装 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。
3. （可选）如果需要，请为远程脚本执行配置 R 辅助角色帐户的数据库访问。
   有关详细信息，请参阅 [安装 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。
3. （可选）如果想要允许从远程数据科学客户端执行 R 脚本，请修改 Azure 虚拟机上的防火墙规则。 有关详细信息，请参阅[取消阻止防火墙](#firewall)。
4. 安装或启用所需的网络库。 有关详细信息，请参阅[添加网络协议](#network)。

## <a name="related-resources"></a>相关资源

[安装 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

