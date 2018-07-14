---
title: 删除工作负荷组 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], delete
- Resource Governor, workload group delete
ms.assetid: d5902c46-5c28-4ac1-8b56-cb4ca2b072d0
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f48df99f595bb313d8ca2406850f75cae82c7020
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274203"
---
# <a name="delete-a-workload-group"></a>删除工作负荷组
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 删除工作负荷组或资源池。  
  
-   **开始之前：**  [限制和局限](#LimitationsRestrictions)、 [权限](#Permissions)  
  
-   **若要删除工作负荷组，请使用：**[对象资源管理器](#DelWGObjEx)、[资源调控器属性](#DelWGRGProp)和 [Transact-SQL](#DelWGTSQL)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 如果工作负荷组中包含活动会话，则不能删除该组。  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 如果工作负荷组包含活动会话，则在调用 ALTER RESOURCE GOVERNOR RECONFIGURE 语句应用更改时，删除工作负荷组或将其移至其他资源池中会失败。 若要避免此问题，可以执行以下操作之一：  
  
-   等待受影响组的所有会话均断开连接，然后重新运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。  
  
-   使用 KILL 命令显式停止受影响的组中的会话，然后重新运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。 如果决定不打算在使用“删除”之后同时在停止活动会话之前显式停止会话，请使用原始名称重新创建组并将组移至原始资源池。  
  
-   重新启动服务器。 完成重新启动过程后，将不会创建已删除的组，并且已移动的组将使用新分配的资源池。  
  
###  <a name="Permissions"></a> Permissions  
 删除工作负荷组需要 CONTROL SERVER 权限。  
  
##  <a name="DelWGObjEx"></a> 使用对象资源管理器删除工作负荷组  
 **使用对象资源管理器删除工作负荷组**  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开对象资源管理器，并依次逐步展开 **“管理”** 节点直至其中包含 **“资源池”**。  
  
2.  在包含要删除的工作负荷组的资源池中，依次逐步展开 **“资源池”** 节点直至其中包含 **“工作负荷组”** 节点。  
  
3.  右键单击工作负荷组，然后单击“删除”。  
  
4.  在 **“删除对象”** 窗口的 **“要删除的对象”** 列表中，将列出工作负荷组。 若要删除工作负荷组，请单击 **“确定”**。  
  
##  <a name="DelWGRGProp"></a> 使用资源调控器属性删除工作负荷组  
 **使用“资源调控器属性”页删除工作负荷组**  
  
1.  在对象资源管理器中，依次向下展开 **“管理”** 节点直至其中包括 **“资源池”**。  
  
2.  右键单击包含要删除的工作负荷组的资源池，然后单击“属性”。 这将打开 **“资源调控器属性”** 页。  
  
3.  在 **“资源池的工作负荷组”** 窗口中，单击要删除的工作负荷组所在的行，再右键单击该行左侧的向右箭头，然后单击“删除”。  
  
4.  若要删除工作负荷组，请单击 **“确定”**。  
  
##  <a name="DelWGTSQL"></a> 使用 Transact-SQL 删除工作负荷组  
 **使用 Transact-SQL 删除工作负荷组**  
  
1.  运行`DROP WORKLOAD GROUP`语句并指定要删除的工作负荷组的名称。  
  
2.  在发出 `ALTER RESOURCE GOVERNOR RECONFIGURE` 语句之前，请确认要删除的工作负荷组中没有活动请求。 如果有活动请求`ALTER RESOURCE GOVERNOR`将失败。 若要避免此问题，您可以执行下列操作之一：  
  
    -   等待工作负荷组中的所有会话都断开连接。  
  
    -   通过使用 `KILL` 命令显式停止工作负荷组中的会话。  
  
    -   重新启动服务器。 工作负荷组将不会重新创建。  
  
    -   在已发出 `DROP WORKLOAD GROUP` 语句但决定不打算显式停止会话以应用更改的情况下，您可以使用在发出 DROP 语句之前组的名称来重新创建组，然后将该组移动到原始资源池。  
  
3.  运行`ALTER RESOURCE GOVERNOR RECONFIGURE`语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 下面的示例删除名为 `groupAdhoc`的工作负荷组。  
  
```  
DROP WORKLOAD GROUP groupAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [资源调控器](resource-governor.md)   
 [创建资源池](create-a-resource-pool.md)   
 [创建工作负荷组](create-a-workload-group.md)   
 [删除资源池](delete-a-resource-pool.md)   
 [DROP WORKLOAD GROUP (Transact-SQL)](/sql/t-sql/statements/drop-workload-group-transact-sql)   
 [DROP RESOURCE POOL (Transact-SQL)](/sql/t-sql/statements/drop-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
