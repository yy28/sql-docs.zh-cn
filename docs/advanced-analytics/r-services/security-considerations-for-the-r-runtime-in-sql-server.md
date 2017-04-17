---
title: "SQL Server 中 R 运行时的安全注意事项 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d01cf234b1695eecd6a8a38b4de60d83b68b2b4d
ms.lasthandoff: 04/11/2017

---
# <a name="security-considerations-for-the-r-runtime-in-sql-server"></a>SQL Server 中 R 运行时的安全注意事项
  本主题提供有关在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中处理 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的安全注意事项概述。  
  
 有关管理服务以及如何设置用于执行 R 脚本的用户帐户的详细信息，请参阅 [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)。  
  
## <a name="use-firewall-to-restrict-network-access-by-r"></a>使用防火墙限制 R 的网络访问  
 在建议的安装方法中，将使用 Windows 防火墙规则来阻止 R 运行时进程的所有出站网络访问。 应创建防火墙规则来防止 R 运行时进程下载程序包或进行其他可能有恶意目的的网络调用。  
  
 强烈建议开启 Windows 防火墙（或你选择的另一种防火墙）以阻止 R 运行时进行网络访问。  
  
 如果使用的是其他防火墙程序，还可以通过为本地用户帐户或用户帐户池所代表的组设置规则来创建规则，以阻止 R 运行时的出站网络连接。   
有关详细信息，请参阅 [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)。  
  
## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>远程计算上下文支持的身份验证方法 
  在创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与远程数据科学客户端之间的连接时，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 现在同时支持进行 Windows 集成身份验证和 SQL 登录。 
  
 例如，如果你要在笔记本电脑上开发 R 解决方案，并且想要在 SQL Server 计算机上执行计算，可通过使用 **rx** 函数基于 Windows 凭据定义连接字符串来在 R 中创建 SQL Server 数据源。 将_计算上下文_从笔记本电脑更改到 SQL Server 计算机时，如果你的 Windows 帐户具有所需的权限，则所有 R 代码将在 SQL Server 计算机上执行。 此外，作为 R 代码的一部分执行的任何 SQL 查询也将在你的凭据下运行。 
 
 尽管 SQL 登录名也可在 SQL Server 数据源的连接字符串中使用，但使用登录名需要 SQL Server 实例允许混合模式身份验证。
 
 ### <a name="implied-authentication"></a>隐式身份验证
  
 一般情况下，[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 在其自己的帐户下启动 R 运行时并执行 R 脚本。 但是，如果 R 脚本进行 ODBC 调用，则 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 将模拟发送命令的用户的凭据，以确保 ODBC 调用不会失败。 这称为*隐式身份验证*。 
 
 > [!IMPORTANT] 
 >
 > 要使隐式身份验证成功，包含辅助角色帐户的 Windows 用户组（默认情况下，为 **SQLRUser**）必须在实例的 master 数据库中有帐户，并且此帐户必须有权连接到该实例。  
  
## <a name="no-support-for-encryption-at-rest"></a>不支持静态加密  
 发送到或接收自 R 运行时的数据不支持透明数据加密。 因此，静态加密 **将不会** 被应用到 R 脚本中使用的任何数据、保存到磁盘中的任何数据，或任何持久的中间结果。  
 
 ## <a name="see-also"></a>另请参阅
 [在此处输入链接说明](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 
  

