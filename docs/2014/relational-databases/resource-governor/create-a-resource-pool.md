---
title: 创建资源池 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5abd2e60f4f9bb5290b47f95349782f8b26ad8bb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85043197"
---
# <a name="create-a-resource-pool"></a>创建资源池
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]创建资源池。  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **若要创建资源池，请使用：**  [SQL Server Management Studio](#CreRPProp)、[Transact-SQL](#CreRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制和局限  
 最大 CPU 百分比必须大于或等于最小 CPU 百分比。 最大内存百分比必须大于或等于最小内存百分比。  
  
 所有资源池的最小 CPU 百分比和最小内存百分比的总和不得超过 100。  
  
###  <a name="permissions"></a><a name="Permissions"></a> 权限  
 创建资源池需要 CONTROL SERVER 权限。  
  
##  <a name="create-a-resource-pool-using-sql-server-management-studio"></a><a name="CreRPProp"></a>使用 SQL Server Management Studio 创建资源池  
 **使用创建资源池[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开对象资源管理器，并依次逐步展开 **“管理”** 节点直至其中并包含 **“资源调控器”**。  
  
2.  右键单击“Resource Governor”****，再单击“属性”****。  
  
3.  在 **“资源池”** 网格中，单击空行中的第一列。 此列标记有星号 (*)。  
  
4.  双击“名称”**** 列中的空单元格。 键入要用于该资源池的名称。  
  
5.  在行中单击或双击要更改的任何其他单元，然后输入新值。  
  
6.  若要保存更改，请单击 **“确定”**。  
  
##  <a name="create-a-resource-pool-using-transact-sql"></a><a name="CreRPTSQL"></a>使用 Transact-sql 创建资源池  
 **使用创建资源池[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  运行指定要设置的属性值的 `CREATE RESOURCE POOL` 语句。  
  
2.  运行**ALTER RESOURCE GOVERNOR 重新配置**语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 下面的示例创建名为 `poolAdhoc`的资源池。  
  
```  
CREATE RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 20);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](resource-governor.md)   
 [启用资源调控器](enable-resource-governor.md)   
 [资源调控器资源池](resource-governor-resource-pool.md)   
 [更改资源池设置](change-resource-pool-settings.md)   
 [删除资源池](delete-a-resource-pool.md)   
 [使用模板配置资源调控器](configure-resource-governor-using-a-template.md)   
 [资源调控器工作负荷组](resource-governor-workload-group.md)   
 [Resource Governor 分类器函数](resource-governor-classifier-function.md)   
 [CREATE RESOURCE POOL (Transact-SQL)](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
