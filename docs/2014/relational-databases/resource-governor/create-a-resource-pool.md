---
title: 创建资源池 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 501252864b260c77697a1bc7cb82a3e415c33916
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028757"
---
# <a name="create-a-resource-pool"></a>创建资源池
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]创建资源池。  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **若要创建资源池，请使用：**[SQL Server Management Studio](#CreRPProp)、[Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 最大 CPU 百分比必须大于或等于最小 CPU 百分比。 最大内存百分比必须大于或等于最小内存百分比。  
  
 所有资源池的最小 CPU 百分比和最小内存百分比的总和不得超过 100。  
  
###  <a name="Permissions"></a> Permissions  
 创建资源池需要 CONTROL SERVER 权限。  
  
##  <a name="CreRPProp"></a> 使用 SQL Server Management Studio 创建资源池  
 **使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开对象资源管理器，并依次逐步展开 **“管理”** 节点直至其中并包含 **“资源调控器”**。  
  
2.  右键单击“Resource Governor”，再单击“属性”。  
  
3.  在 **“资源池”** 网格中，单击空行中的第一列。 此列标记有星号 (*)。  
  
4.  双击“名称”列中的空单元格。 键入要用于该资源池的名称。  
  
5.  在行中单击或双击要更改的任何其他单元，然后输入新值。  
  
6.  若要保存更改，请单击 **“确定”**。  
  
##  <a name="CreRPTSQL"></a> 使用 Transact-SQL 创建资源池  
 **使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  运行指定要设置的属性值的 `CREATE RESOURCE POOL` 语句。  
  
2.  运行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 下面的示例创建名为 `poolAdhoc`的资源池。  
  
```  
CREATE RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 20);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [资源调控器](resource-governor.md)   
 [启用资源调控器](enable-resource-governor.md)   
 [资源调控器资源池](resource-governor-resource-pool.md)   
 [更改资源池设置](change-resource-pool-settings.md)   
 [删除资源池](delete-a-resource-pool.md)   
 [使用模板配置资源调控器](configure-resource-governor-using-a-template.md)   
 [资源调控器工作负荷组](resource-governor-workload-group.md)   
 [资源调控器分类器函数](resource-governor-classifier-function.md)   
 [CREATE RESOURCE POOL (Transact-SQL)](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
