---
title: "管理和监视 R 解决方案 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85d8524646ad367c5b6e6132287de3ff370422e9
ms.lasthandoff: 04/11/2017

---
# <a name="managing-and-monitoring-r-solutions"></a>管理和监视 R 解决方案
  数据库管理员必须将存在竞争的项目和优先级集成到一个联系点中，即数据库服务器。 他们不仅需要为数据科学家提供数据访问权限，还需要为各类报表开发者、业务分析人员和业务数据使用者提供数据访问权限，同时还负责维护操作和报告数据存储的运行状况。 在企业中，DBA 是构建和部署有效的数据科学基础结构的重要组成部分。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 为支持数据科学角色的数据库管理员带来了许多好处。  
  
-   **安全性。** [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的体系结构可保证数据库的安全性，并将 R 会话执行从数据库实例操作中隔离出来。  
  
     你可以指定有权执行 R 脚本的人员，并确保使用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中定义的同一安全角色来管理 R 作业中使用的数据。  
  
-   **可靠性。** R 会话是在单独的进程中执行，即使 R 会话遇到问题，也可以确保你的服务器继续照常运行。 低权限物理用户帐户用于包含和隔离 R 实例。   
  
-   **资源调控。** 你可以控制分配给 R 运行时的资源量，以防止海量计算降低服务器的整体性能。  
  
  
## <a name="in-this-section"></a>本节内容  
 [监视 R Services](../../advanced-analytics/r-services/monitoring-r-services.md)
 
 [R Services 的资源调控](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
 
[安装和管理 R 包](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)
  
[配置](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 

+ [配置和管理高级分析扩展](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)  
  
+  [修改 SQL Server R Services 的用户帐户池](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  

 [SQL Server 中 R 运行时的安全注意事项](../../advanced-analytics/r-services/security-considerations-for-the-r-runtime-in-sql-server.md)  
  
 
  
## <a name="see-also"></a>另请参阅  
 [SQL Server R 服务功能和任务](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
  

