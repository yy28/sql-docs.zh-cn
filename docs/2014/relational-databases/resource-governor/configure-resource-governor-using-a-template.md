---
title: 使用模板配置资源调控器 | Microsoft Docs
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
- Resource Governor, templates
ms.assetid: f342dec2-d1d6-483e-b44e-98eb7d168b5e
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6ac998eb2ad98705fc9ac72fc69d7fbfb167bb5b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124534"
---
# <a name="configure-resource-governor-using-a-template"></a>使用模板配置资源调控器
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中提供的模板配置资源调控器。  
  
-   **开始之前：**  [权限](#Permissions)  
  
-   **若要创建工作负荷组，使用：**  [模板](#ConfRGTemplate)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 使用下列步骤可打开和修改创建资源池和资源池的工作负荷组的模板。 此外，该模板还可以创建分类器用户定义函数，以将新的连接传送到默认组或用户创建的工作负荷组。  
  
###  <a name="Permissions"></a> Permissions  
 模板中的资源调控器 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句需要 CONTROL SERVER 权限。  
  
##  <a name="ConfRGTemplate"></a> 使用模板配置资源调控器  
 **使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“视图”  菜单上，单击“模板资源管理器” 。  
  
2.  在**模板资源管理器**中，展开“资源调控器”，然后双击“配置资源调控器”。  
  
3.  在 **“连接到数据库引擎”** 中，输入所需信息，然后单击 **“确定”**。 查询编辑器中提供模板 Configure Resource Governor.sql。 使用此模板可创建和配置资源池、工作负荷组和分类器函数。  
  
4.  若要更改模板中的值，请按 CTRL+SHIFT+M。 在 **“指定模板参数的值”** 窗口中，输入要使用的值。  
  
5.  若要保存对该模板所做的更改，请单击 **“确定”**。  
  
6.  若要运行查询，请单击 **“执行”**。  
  
## <a name="see-also"></a>请参阅  
 [资源调控器](resource-governor.md)   
 [启用资源调控器](enable-resource-governor.md)   
 [资源调控器资源池](resource-governor-resource-pool.md)   
 [资源调控器工作负荷组](resource-governor-workload-group.md)   
 [资源调控器分类器函数](resource-governor-classifier-function.md)   
 [查看资源调控器属性](view-resource-governor-properties.md)   
 [CREATE RESOURCE POOL (Transact-SQL)](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [CREATE WORKLOAD GROUP (Transact-SQL)](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [CREATE FUNCTION (Transact-SQL)](/sql/t-sql/statements/create-function-transact-sql)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
