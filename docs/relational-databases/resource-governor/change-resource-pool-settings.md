---
title: 更改资源池设置 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool alter
- resource pools [SQL Server], alter
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 328d61171c28f89083712c7f46c7b97394a7de84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68136997"
---
# <a name="change-resource-pool-settings"></a>更改资源池设置
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]更改资源池设置。  
  
-   **开始之前：**[限制和局限](#LimitationsRestrictions)、[权限](#Permissions)  
  
-   若要更改资源池的设置，请使用：[SQL Server Management Studio](#ChgRPProp)、[Transact-SQL](#ChgRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 最大 CPU 百分比必须大于或等于最小 CPU 百分比。 最大内存百分比必须大于或等于最小内存百分比。  
  
 所有资源池的最小 CPU 百分比和最小内存百分比的总和不得超过 100。  
  
###  <a name="Permissions"></a> 权限  
 更改资源池设置需要 CONTROL SERVER 权限。  
  
##  <a name="ChgRPProp"></a> 使用 SQL Server Management Studio 更改资源池设置  
 **使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开对象资源管理器，然后依次逐步展开“管理”  节点直至其中包含“资源池” 。  
  
2.  右键单击要修改的资源池，然后单击“属性”。  
  
3.  在 **“资源调控器属性”** 页中，如果资源池所在的行未自动选中，则在 **“资源池”** 网格内将其选中。  
  
4.  在行中单击或双击要更改的单元，然后输入新值。  
  
5.  若要保存更改，请单击 **“确定”**。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="ChgRPTSQL"></a> 使用 Transact-SQL 更改资源池设置  
 **使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  运行指定要更改的属性值的 **ALTER RESOURCE POOL** 或 **ALTER EXTERNAL RESOURCE POOL** 语句。  
  
2.  运行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 以下示例更改名为 `poolAdhoc`的资源池的最大 CPU 百分比设置。  
  
```  
ALTER RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)   
 [启用资源调控器](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [创建资源池](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [删除资源池](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [资源调控器工作负荷组](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [资源调控器分类器函数](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
