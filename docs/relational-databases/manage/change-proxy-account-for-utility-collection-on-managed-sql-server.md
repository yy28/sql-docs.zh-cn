---
title: 更改托管 SQL Server 上实用工具收集的代理帐户 | Microsoft Docs
description: 了解如何使用 SQL Server Management Studio 更改 SQL Server 的托管实例上的实用工具收集组的代理帐户。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 103092d54d1b03405e91e5f1ae385bd396faebba
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868632"
---
# <a name="change-proxy-account-for-utility-collection-on--managed-sql-server"></a>更改托管 SQL Server 上实用工具收集的代理帐户
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  本主题介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中更改 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的托管实例上的实用工具收集组的代理帐户。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>更改 SQL Server 的托管实例上的实用工具收集组的代理帐户  
  
1.  从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。  
  
    -   在 SSMS 的 **“实用工具资源管理器”** 中，单击 **“托管实例”** 节点。  
  
    -   在“实用工具资源管理器”列表视图中，右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称，然后选择“删除托管实例…” 。有关详细信息，请参阅 [从 SQL Server 实用工具中删除 SQL Server 的实例](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)。  
  
2.  再次在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中注册 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  

    -   在 SSMS 的“实用工具资源管理器”中，右键单击“托管实例”节点，然后选择“添加托管实例…”  。  
  
    -   按照提示完成向导并且指定新的代理帐户。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 实用工具的功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 实用工具故障排除](/previous-versions/sql/sql-server-2016/ee210592(v=sql.130))  
  
