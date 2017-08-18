---
title: "安装 SQL Server 数据库引擎 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
caps.latest.revision: 45
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 192549457850c9c24fd72ce3f205e0ddedfe1d12
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-database-engine"></a>安装 SQL Server 数据库引擎
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件是用于存储、处理数据和保证数据安全的核心服务。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 提供受控的访问和快速事务处理，以满足企业中要求极高、大量使用数据的应用程序的要求。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持在同一台计算机上最多存在 50 个 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例。 若要创建典型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装，请参阅[使用安装向导安装 SQL Server 2016（安装程序）](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
 **重要提示** 对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。  
  
 在 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导的“要安装的组件”页上选择** 数据库引擎” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，将安装下列功能：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   复制 - 是一个可选组件  
  
-   全文搜索 - 是一个可选组件  
  
-   Data Quality Services — 一个可选组件  
  
    > [!NOTE]  
    >  在此版本中，在安装程序中选中“Data Quality Services”复选框不会安装 Data Quality Services (DQS) 服务器。 您必须执行其他安装后步骤以安装 DQS 服务器。 有关详细信息，请参阅 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)。  
  
 下列附加功能是许多典型用户应用场景的可选项：  
  
-   数据质量客户端  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   连接组件  
  
-   编程模型  
  
-   管理工具  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   文档组件  
  
> [!NOTE]  
>  默认情况下，不会将示例数据库和示例代码作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的一部分进行安装。 若要安装示例数据库和示例代码，请参阅 [CodePlex 网站](http://go.microsoft.com/fwlink/?LinkId=87843)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [SQL Server 2016 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)   
 [高可用性解决方案 (SQL Server)](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [使用安装向导（安装程序）升级到 SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

