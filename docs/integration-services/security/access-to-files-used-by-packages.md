---
title: "对包使用的文件的访问 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SSIS 包, 安全性"
  - "包 [Integration Services], 安全性"
  - "配置文件 [Integration Services]"
  - "检查点文件"
  - "Integration Services 包, 安全性"
  - "日志 [Integration Services], 安全性"
  - "文件 [Integration Services], 安全性"
  - "SQL Server Integration Services 包, 安全性"
ms.assetid: 2e3ddea9-5289-4289-a70e-11c018f34977
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# 对包使用的文件的访问
  包保护级别不保护存储在包以外的文件。 这些文件包括下面的文件：  
  
-   配置文件  
  
-   检查点文件  
  
-   日志文件  
  
 这些文件必须单独进行保护，尤其是在它们包括敏感的信息时。  
  
## 配置文件  
 如果配置中有敏感的信息，例如登录名和密码信息，则应当考虑将配置保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或使用访问控制列表 (ACL) 来限制对存储文件的位置或文件夹的访问，并只允许访问某些帐户。 通常，可以向允许其运行包的帐户以及负责管理包和排除包的故障的帐户授予访问权，这些权限可能包括检查配置、检查点和日志文件的内容。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了更安全的存储方式，因为它在服务器和数据库级别提供保护。 若要将配置保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置类型。 若要保存到文件系统，请使用 XML 配置类型。  
  
 有关详细信息，请参阅[包配置](../../integration-services/packages/package-configurations.md)、[创建包配置](../../integration-services/packages/create-package-configurations.md)和[有关 SQL Server 安装的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)。  
  
## 检查点文件  
 同样，如果包所使用的检查点文件包含敏感信息，则应使用访问控制列表 (ACL) 来保证文件存储位置或所在文件夹的安全。 检查点文件用于保存有关包进度的当前状态信息和变量的当前值。 例如，包中可能包含含有电话号码的自定义变量。 有关详细信息，请参阅 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)。  
  
## 日志文件  
 写入文件系统的日志项也应使用访问控制列表 (ACL) 进行保护。 日志项也可存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中，受 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全机制的保护。 日志项可能包含敏感信息。例如，如果包中包含构造 SQL 语句的执行 SQL 任务，而所构造的 SQL 语句又引用电话号码，则对应于该 SQL 语句的日志项就会包含电话号码。 SQL 语句还可能泄漏数据库中有关表和列名的私有信息。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
  