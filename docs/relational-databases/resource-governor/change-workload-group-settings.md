---
title: 更改工作负荷组设置 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], alter
- Resource Governor, workload group alter
ms.assetid: 73b6109c-2ad0-4915-b11b-d40d5a0fdc25
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 99e93baf0ee07f7d60de147c90b52de9322b1805
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380498"
---
# <a name="change-workload-group-settings"></a>更改工作负荷组设置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]更改工作负荷组设置。  
  
-   **开始之前：**[限制和局限](#LimitationsRestrictions)、[权限](#Permissions)  
  
-   **若要更改工作负荷组的设置，请使用：**[SQL Server Management Studio](#ChgWGProp)、[Transact-SQL](#ChgWGTSQL)  
  
## <a name="before-you-begin"></a>开始之前  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 您可以更改默认工作负荷组和用户定义的工作负载组的设置。  
  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 对非对齐的分区表创建索引所占用的内存与涉及的分区数成正比。 如果所需的内存总量超过工作负荷组设置为每个查询设定的限制 (REQUEST_MAX_MEMORY_GRANT_PERCENT)，则这种索引创建可能会失败。 由于默认工作负荷组允许查询超过每个查询的限制，并在开始时使用所需的最低内存以便与 SQL Server 2005 保持兼容，因此，如果默认资源池配置了足够多的内存总量以运行此类查询，则用户或许能够在默认工作负荷组中运行相同的索引创建。  
  
 允许索引创建操作使用比最初授予的工作区内存多的工作区内存，以便提高性能。 这个特别处理由资源调控器支持，然而，最初授予及任何其他内存授予都受工作负荷组和资源池设置的限制。  
  
###  <a name="Permissions"></a> Permissions  
 更改工作负荷组设置需要 CONTROL SERVER 权限。  
  
##  <a name="ChgWGProp"></a> 使用 SQL Server Management Studio 更改工作负荷组设置  
 **使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在对象资源管理器中，依次逐步展开 **“管理”** 节点直至其中包含要修改的工作负荷组的 **“工作负荷组”** 文件夹。  
  
2.  右键单击要修改的工作负荷组，然后单击“属性”。  
  
3.  在 **“资源调控器属性”** 页中，如果工作负荷组所在的行未自动选中，则在 **“资源池的工作负荷组”** 网格内将其选中。  
  
4.  在行中单击或双击要更改的单元，然后输入新值。  
  
5.  若要保存更改，请单击 **“确定”**。  
  
##  <a name="ChgWGTSQL"></a> 使用 Transact-SQL 更改工作负荷组设置  
 **使用 Transact-SQL 更改工作负荷组设置**  
  
1.  运行 ALTER WORKLOAD GROUP 语句，指定要更改的属性值。  
  
2.  运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 以下示例更改名为 `groupAdhoc`的工作负荷组的最大内存授予百分比设置。  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
WITH (REQUEST_MAX_MEMORY_GRANT_PERCENT = 30);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)   
 [创建工作负荷组](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [创建资源池](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [更改资源池设置](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [ALTER WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [ALTER RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
