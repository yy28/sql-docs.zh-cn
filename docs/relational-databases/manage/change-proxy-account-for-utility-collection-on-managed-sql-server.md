---
title: "更改托管 SQL Server 上实用工具收集的代理帐户 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45a8f3cef6d892120a766672f85361621a534348
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="change-proxy-account-for-utility-collection-on--managed-sql-server"></a>更改托管 SQL Server 上实用工具收集的代理帐户
  本主题介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中更改 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的托管实例上的实用工具收集组的代理帐户。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>更改 SQL Server 的托管实例上的实用工具收集组的代理帐户  
  
1.  从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。  
  
    -   在 SSMS 的 **“实用工具资源管理器”** 中，单击 **“托管实例”** 节点。  
  
    -   在“实用工具资源管理器”列表视图中，右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称，然后选择“删除托管实例…”。 有关详细信息，请参阅[从 SQL Server 实用工具中删除 SQL Server 的实例](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)。  
  
2.  再次在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中注册 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
    -   在 SSMS 的“实用工具资源管理器”中，右键单击“托管实例”节点，然后选择“添加托管实例…”。  
  
    -   按照提示完成向导并且指定新的代理帐户。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 实用工具的功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 实用工具故障排除](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
