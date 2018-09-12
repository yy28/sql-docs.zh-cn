---
title: 更改实用工具收集的代理帐户在 SQL Server （SQL Server 实用工具） 的托管实例设置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4191573cac0b75fb35bea3cf83f47ec13425e17c
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811333"
---
# <a name="change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server-sql-server-utility"></a>在 SQL Server 的托管实例上更改实用工具收集组的代理帐户（SQL Server 实用工具）
  本主题介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中更改 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的托管实例上的实用工具收集组的代理帐户。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>更改 SQL Server 的托管实例上的实用工具收集组的代理帐户  
  
1.  从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。  
  
    -   在 SSMS 的 **“实用工具资源管理器”** 中，单击 **“托管实例”** 节点。  
  
    -   在“实用工具资源管理器”列表视图中，右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称，然后选择“删除托管实例…”。 有关详细信息，请参阅[从 SQL Server 实用工具中删除 SQL Server 的实例](remove-an-instance-of-sql-server-from-the-sql-server-utility.md)。  
  
2.  再次在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中注册 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
    -   在 SSMS 的“实用工具资源管理器”中，右键单击“托管实例”节点，然后选择“添加托管实例…”。  
  
    -   按照提示完成向导并且指定新的代理帐户。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 实用工具的功能和任务](sql-server-utility-features-and-tasks.md)   
 [SQL Server 实用工具故障排除](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
