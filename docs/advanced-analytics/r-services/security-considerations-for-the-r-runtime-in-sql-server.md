---
title: "SQL Server 中 R 运行时的安全注意事项 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# SQL Server 中 R 运行时的安全注意事项
  本主题提供有关在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中处理 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的安全注意事项概述。  
  
 有关管理服务以及如何设置用于执行 R 脚本的用户帐户的详细信息，请参阅 [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)。  
  
## 使用防火墙限制 R 的网络访问  
 在建议的安装方法中，将使用 Windows 防火墙规则来阻止 R 运行时进程的所有出站网络访问。 应创建防火墙规则来防止 R 运行时进程下载程序包或进行其他可能有恶意目的的网络调用。  
  
 强烈建议开启 Windows 防火墙（或你选择的另一种防火墙）以阻止 R 运行时进行网络访问。  
  
 如果使用的是其他防火墙程序，还可以通过为本地用户帐户或用户帐户池所代表的组设置规则来创建规则，以阻止 R 运行时的出站网络连接。   
有关详细信息，请参阅 [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)。  
  
## 支持远程计算上下文的身份验证方法 
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 现在支持 Windows 集成身份验证和 SQL 登录名在之间创建连接时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和远程数据科学客户端。 
  
 例如，如果您在您的便携式计算机上开发 R 解决方案，并且想要在 SQL Server 计算机上执行计算，您将创建 SQL Server 数据源在 R 中，通过使用 **rx** 函数和定义的连接字符串基于您的 Windows 凭据。 当你更改 _计算上下文_ 从 SQL Server 计算机到便携式计算机，如果您的 Windows 帐户具有所需的权限，所有的 R 代码将执行 SQL Server 计算机上。 此外，将在您的凭据以及下运行的 R 代码的一部分执行的任何 SQL 查询。 
 
 尽管 SQL 登录名还在连接字符串中使用的 SQL Server 数据源，但使用一个登录名需要 SQL Server 实例允许混合的模式身份验证。
 
 ### 隐式身份验证
  
 一般情况下在 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 开始 R 运行时并执行其自己帐户的 R 脚本。 但是，如果 R 脚本通过 ODBC 调用， [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 将模拟发送命令，以确保 ODBC 调用不会失败的用户的凭据。 这称为 *暗示的保证身份验证*。 
 
 > [!IMPORTANT] 
 >
 > 隐式身份验证是成功的包含工作人员帐户的 Windows 用户组 (默认情况下， **SQLRUser**) 的实例，此帐户必须分配有权连接到的实例则必须在 master 数据库中的帐户。  
  
## 不支持静态加密  
 发送到或接收自 R 运行时的数据不支持透明数据加密。 因此，静态加密 **将不会** 被应用到 R 脚本中使用的任何数据、保存到磁盘中的任何数据，或任何持久的中间结果。  
 
 ## 另请参阅
 [链接在此输入说明](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 
  