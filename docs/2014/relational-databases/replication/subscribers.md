---
title: 订阅服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.newsubwizard.subscribers.f1
helpviewer_keywords:
- Subscribers [SQL Server replication]
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
caps.latest.revision: 25
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c1ab2fd4a3e7eff9f368ebbd85da8c82605e1341
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128285"
---
# <a name="subscribers"></a>订阅服务器
  指定接收对所选发布的订阅的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。  
  
## <a name="options"></a>“常规”  
 **订阅服务器**  
 选中网格中的复选框可以启用相应的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源作为 **“发布”** 页上所选发布的订阅服务器。 如果没有列出订阅服务器，请单击 **“添加订阅服务器”** 或 **“添加 SQL Server 订阅服务器”**。  
  
 **订阅数据库**  
 此列中显示的信息和其中可用的操作取决于 **“订阅服务器”** 列中所列的订阅服务器的类型：  
  
-   对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器，请从 **“订阅数据库”** 列表中选择订阅数据库，或从同一列表中选择 **“新建数据库”** 命令来创建新的数据库。  
  
    > [!NOTE]  
    >  若要启用发布服务器作为订阅服务器，则订阅数据库与发布数据库必须属于不同的数据库。  
  
-   对于非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器，不显示订阅数据库。 请在 **“添加非 SQL Server 订阅服务器”** 对话框的 **“数据源名称”** 字段中指定数据库以及其他连接信息。 若要显示此对话框，请单击 **“添加订阅服务器”** ，再单击 **“添加非 SQL Server 订阅服务器”**。  
  
 **“添加订阅服务器”**  
 向可以启用为订阅服务器的服务器列表中添加服务器。 如果以下条件全部为真，则显示此按钮：  
  
-   所选择的发布是不支持更新订阅的快照或事务发布。  
  
    > [!NOTE]  
    >  如果正在订阅的发布有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅，并且尚未为非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器启用发布，则不能添加非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅。  
  
-   订阅是推送订阅。  
  
-   所选发布的发布服务器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本。  
  
 单击 **“添加订阅服务器”** 将显示一个菜单，其中包含两个选项： **“添加 SQL Server 订阅服务器”** 和 **“添加非 SQL Server 订阅服务器”**。 单击 **“添加非 SQL Server 订阅服务器”** 可以添加 Oracle 或 IBM DB2 订阅服务器。  
  
 **“添加 SQL Server 订阅服务器”**  
 向可以启用为订阅服务器的服务器列表中添加服务器。 如果以下一个或多个条件为真，则显示此按钮：  
  
-   所选择的发布是合并发布，或者是支持更新订阅的快照或事务发布。  
  
-   订阅是请求订阅。  
  
-   所选发布的发布服务器的版本早于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 对于早期版本，只有当以下一个或多个条件为真时才会显示该按钮：  
  
    -   您是发布服务器上 **sysadmin** 固定服务器角色的成员。  
  
    -   已在 **“发布服务器属性”** 对话框的 **“订阅服务器”** 页上添加了该订阅服务器。  
  
    -   发布允许匿名订阅。  
  
## <a name="see-also"></a>请参阅  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  