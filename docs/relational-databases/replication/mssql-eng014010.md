---
title: MSSQL_ENG014010 | Microsoft Docs
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014010 error
ms.assetid: 6ea84f2f-e7a2-4028-9ea9-af0d2eba660e
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 82df494fef69095800b93252dd6f474be0566c95
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng014010"></a>MSSQL_ENG014010
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14010|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|未将服务器“%s”定义为订阅服务器。|  
  
## <a name="explanation"></a>解释  
 复制要求一个拓扑中的所有服务器都使用具有可选实例名称的计算机名称（如果为群集实例，则为具有可选实例名称的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 虚拟服务器名称）来注册。 `SELECT @@SERVERNAME` 为拓扑中每个服务器返回的值必须与具有可选实例名称的计算机名称或虚拟服务器名称相匹配，复制才能正常运行。  
  
 如果已按 IP 地址或完全限定域名 (FQDN) 注册了任意 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，将不支持复制。 配置复制时，如果已在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中通过 IP 地址或 FQDN 注册了 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 实例，则可能会引发此错误。  
  
## <a name="user-action"></a>用户操作  
 验证拓扑中的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例都已正确注册。 如果计算机的网络名称和 SQL Server 实例的名称不一致，则：  
  
-   添加 SQL Server 实例名称作为有效的网络名称。 一种设置备用网络名称的方法是将其添加到本地主机文件中。 默认情况下，本地主机文件位于 WINDOWS\system32\drivers\etc 或 WINNT\system32\drivers\etc 中。有关详细信息，请参阅 Windows 文档。  
  
     例如，如果计算机名称为 comp1，IP 地址为 10.193.17.129，实例名称为 inst1/instname，则将以下条目添加到主机文件中：  
  
     10.193.17.129 inst1  
  
-   删除复制，注册每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，然后重新建立复制。 如果 @@SERVERNAME 的值对于某个非群集实例是不正确的，请执行下列步骤：  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     执行 [sp_addserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) 存储过程后，必须重启 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务，对 @@SERVERNAME 的更改才能生效。  
  
     如果 @@SERVERNAME 的值对于某个群集实例是不正确的，则必须使用群集管理器更改该名称。 有关详细信息，请参阅 [AlwaysOn 故障转移群集实例 (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)实例的故障转移群集实例。  
  
## <a name="see-also"></a>另请参阅  
 [@@SERVERNAME (Transact-SQL)](../../t-sql/functions/servername-transact-sql.md)   
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

