---
title: "禁用资源调控器 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, disabling
ms.assetid: 2c2d2db0-34a5-4f50-b783-17693e3ce3f1
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 47091df9ec1318e7bb66ef1a32346c7445b4abd6
ms.lasthandoff: 04/11/2017

---
# <a name="disable-resource-governor"></a>禁用资源调控器
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 禁用资源调控器。  
  
-   **开始之前：**  [限制和局限](#LimitationsRestrictions)、 [权限](#Permissions)  
  
-   **若要禁用资源调控器，请使用：**[对象资源管理器](#RGOffObjEx)、[资源调控器属性](#RGOffProp)和 [Transact-SQL](#RGOffTSQL)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 禁用资源调控器会产生下列结果：  
  
-   不运行分类器函数。  
  
-   所有新连接被自动分类到默认工作负荷组中。  
  
-   系统发起的请求被分类到内部工作负荷组中。  
  
-   所有现有的工作负荷组和资源池设置被重置为其默认值。 在这种情况下，到达限制时不触发任何事件。  
  
-   正常的系统监视不受影响。  
  
-   可以进行配置更改，但是这些更改直到启用资源调控器之后才会生效。  
  
-   在重新启动 SQL Server 时，资源调控器不会加载其配置，而是只具有默认的和内部的工作负荷组和资源池。  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 在用户事务中时，您不能使用 **ALTER RESOURCE GOVERNOR** 语句禁用资源调控器。  
  
###  <a name="Permissions"></a> 权限  
 禁用资源调控器需要 CONTROL SERVER 权限。  
  
##  <a name="RGOffObjEx"></a> 使用对象资源管理器禁用资源调控器  
 **使用对象资源管理器禁用资源调控器**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中打开对象资源管理器，并依次逐步展开 **“管理”** 节点直至 **“资源调控器”**。  
  
2.  右键单击“资源调控器”，再单击“禁用”。  
  
##  <a name="RGOffProp"></a> 使用资源调控器属性禁用资源调控器  
 **使用“资源调控器属性”页禁用资源调控器**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中打开对象资源管理器，并依次逐步展开 **“管理”** 节点直至 **“资源调控器”**。  
  
2.  右键单击“资源调控器”，然后单击“属性”，这将打开“资源调控器属性”页。  
  
3.  单击 **“启用资源调控器”** 复选框，确保未选中该框，然后单击 **“确定”**。  
  
##  <a name="RGOffTSQL"></a> 使用 Transact-SQL 禁用资源调控器  
 **使用 Transact-SQL 禁用资源调控器**  
  
1.  运行 **ALTER RESOURCE GOVERNOR DISABLE** 语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 以下示例启用资源调控器。  
  
```  
ALTER RESOURCE GOVERNOR DISABLE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)   
 [启用资源调控器](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [资源调控器工作负荷组](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [资源调控器分类器函数](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
