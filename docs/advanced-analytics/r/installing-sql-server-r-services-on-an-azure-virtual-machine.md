---
title: "在 Azure 虚拟机上安装 SQL Server 机器学习功能 |Microsoft 文档"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: af558a4792eed6d38eb03fc80d230c5ada8d7fb5
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="installing-sql-server-machine-learning-features-on-an-azure-virtual-machine"></a>安装 SQL Server 机器学习 Azure 虚拟机上的功能
 
如果你部署 Azure 虚拟机包含[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，现在可以选择机器学习，作为一项功能时创建的 VM 要添加到的实例。

+ [创建新的 VM，其中包括 SQL Server 2016 和 R Services](#new)
+ [向现有 SQL Server 2016 的虚拟机添加机器学习功能](#existing)

> [!NOTE]
> 虚拟机了现在可用于 SQL Server 2017 ！ 请参阅[此公告](https://azure.microsoft.com/blog/announcing-new-azure-vm-images-sql-server-2017-on-linux-and-windows/)有关详细信息。
> 
> R 是还可作为在 Azure SQL 数据库中的预览功能。 有关详细信息，请参阅[Azure SQL 数据库中使用 R](../r/using-r-in-azure-sql-database.md)。

## <a name="create-a-new-sql-server-2017-virtual-machine"></a>创建新的 SQL Server 2017 虚拟机

若要在 SQL Server 2017 中使用 R 或 Python，请务必获取基于 Windows 的虚拟机。 [!INCLUDE[sscurrentlong-md](../../includes/sscurrentlong-md.md)]在 Linux 上支持快速[本机评分](../sql-native-scoring.md)使用 T-SQL 的预测函数中，但其他机器学习功能将不可用尚未在此版本中。

有关 SQL Server 虚拟机产品/服务的列表，请参阅此文章：[概述的 SQL Server 在 Azure 虚拟机 (Windows)](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)。

### <a name="new"></a>使用机器学习创建新的 SQL Server Enterprise 虚拟机

1. 在 Azure 门户中，单击虚拟机，然后单击新建。
2. 选择 SQL Server 自 2017 年 1 Enterprise Edition。
3. 配置服务器名称和帐户权限，然后选择定价计划。
4. 在**SQL Server 设置**(VM 安装向导中的步骤 4)，找到**机器学习服务 （高级分析）**单击**启用**。
5. 查看用于验证的摘要，然后单击“确定”。
6. 虚拟机准备就绪后，请与它建立连接，然后打开预先安装的 SQL Server Management Studio。 机器学习已准备好运行。
7. 若要验证是否可运行，可以打开一个新的查询窗口，然后运行如下所示的简单语句（使用 R 生成从 1 到 10 的序列号）。

    ```
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
    ```

6. 如果你计划从远程数据科学客户端连接到的实例，完成[其他步骤](#additional-steps)根据需要。

### <a name="disable-machine-learning-features-on-a-sql-server-vm"></a>禁用 SQL Server 虚拟机上的机器学习功能

你还可以启用或禁用现有的 SQL Server 虚拟机上的功能在任何时间。

1. 打开虚拟机边栏选项卡。
2. 单击“设置”，然后选择“SQL Server 配置”。
3. 对功能进行更改并应用。

### <a name="existing"></a>将 R Services 添加到现有的 SQL Server 2016 Enterprise VM

如果你创建 Azure 虚拟机而无需机器学习中包含 SQL Server，你可以通过执行以下步骤添加该功能：

1. 重新运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序，在向导的“服务器配置”页上添加该功能。
2. 启用外部脚本执行并重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 有关详细信息，请参阅[设置 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。
3. （可选）如果需要，请为远程脚本执行配置 R 辅助角色帐户的数据库访问。
   有关详细信息，请参阅 [安装 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。
3. （可选）如果想要允许从远程数据科学客户端执行 R 脚本，请修改 Azure 虚拟机上的防火墙规则。 有关详细信息，请参阅[取消阻止防火墙](#firewall)。
4. 安装或启用所需的网络库。 有关详细信息，请参阅[添加网络协议](#network)。

## <a name="additional-steps"></a>额外的步骤

如果希望远程客户端访问服务器作为远程 SQL Server 计算上下文，则需要执行一些其他步骤。

### <a name="firewall"></a>取消阻止防火墙

默认情况下，Azure 虚拟机上的防火墙包括阻止网络访问本地用户帐户的规则。

必须禁用此规则，以确保可以访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从远程数据科学客户端的实例。  否则，你的机器学习代码无法在使用虚拟机的工作区的计算上下文中执行。

若要启用从远程数据科学客户端的访问：

1. 在虚拟机上打开“高级安全 Windows 防火墙”。
2. 选择“出站规则”。
3. 禁用以下规则：
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>启用远程客户端的 ODBC 回调

如果希望客户端调用服务器将需要发出 ODBC 查询作为其机器学习解决方案的一部分，则必须确保快速启动板可代表远程客户端的 ODBC 调用。 为此，必须允许 Launchpad 使用的 SQL 辅助角色帐户登录到实例。
有关详细信息，请参阅 [安装 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。

### <a name="network"></a>添加网络协议

+ 启用命名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 对客户端与服务器计算机之间的连接以及某些内部连接使用命名管道协议。 如果未启用命名管道，必须同时在 Azure 虚拟机以及连接到服务器的任何数据科学客户端上安装并启用命名管道。
  
+ 启用 TCP/IP

  TCP/IP 是必需的环回连接。 如果你收到以下错误，虚拟机支持实例上启用 TCP/IP:

  "DBNETLIB;SQL Server 不存在或拒绝访问"

## <a name="related-resources"></a>相关资源

[在 Azure SQL Database 中使用 R](../r/using-r-in-azure-sql-database.md)