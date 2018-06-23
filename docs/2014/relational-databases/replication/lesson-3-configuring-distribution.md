---
title: 第 3 课：配置分发 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ab6c3ab7b14b8e7443b9ac6b39225aa02671fa88
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025465"
---
# <a name="lesson-3-configuring-distribution"></a>第 3 课：配置分发
  在本课中，将在发布服务器中配置分发，并设置所需的发布数据库和分发数据库权限。 如果已经配置了分发服务器，则必须在开始本课之前先禁用发布和分发。 如果必须保留现有复制拓扑，请不要执行该操作。  
  
 使用远程分发服务器配置发布服务器不属于本教程讨论的范畴。  
  
### <a name="configuring-distribution-at-the-publisher"></a>在发布服务器中配置分发  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  右键单击“复制”文件夹，然后单击“配置分发”。  
  
    > [!NOTE]  
    >  如果连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的是 **localhost**，而不是实际服务器名称，则系统会向你显示一个警告提示，指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法连接到服务器 **'localhost'**。 在警告对话框中单击“确定”。 在“连接到服务器”对话框中，将“服务器名称”从 **localhost** 更改为你的服务器的名称。 单击 **“连接”**。  
  
     此时分发配置向导启动。  
  
3.  上**分发服务器**页上，选择*****\<ServerName >*** 将充当自己的分发服务器;SQL Server 将创建分发数据库和日志**，然后单击**下一步**。  
  
4.  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未运行，则在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]“代理启动”页上，选择“是”**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，将**  代理服务配置为自动启动。 单击“下一步” 。  
  
5.  在“快照文件夹”文本框中，输入 \\\\\<Machine_Name>\repldata（其中 \<Machine_Name> 是发布服务器的名称），然后单击“下一步”。  
  
6.  接受向导剩余页上的默认值。  
  
7.  单击“完成”以启用分发。  
  
### <a name="setting-database-permissions-at-the-publisher"></a>在发布服务器中设置数据库权限  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，展开“安全性”，右键单击“登录名”，然后选择“新建登录名”。  
  
2.  在“常规”页上单击“搜索”，在“输入要选择的对象名称”框中输入 \<Machine_Name>\repl_snapshot（其中 \<Machine_Name> 是本地发布服务器的名称），单击“检查名称”，然后单击“确定”。  
  
3.  在“用户映射”页上，在“映射到此登录名的用户”列表中选择“分发”和 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
     在**数据库角色成员身份**列表中，选择`db_owner`这两个数据库的登录名的角色。  
  
4.  单击“确定”创建登录名。  
  
5.  重复步骤 1 至 4，为本地 repl_logreader 帐户创建登录名。 此登录名也必须映射到的成员用户`db_owner`中的固定的数据库角色**分发**和**AdventureWorks**数据库。  
  
6.  重复步骤 1 至 4，为本地 repl_distribution 帐户创建登录名。 此登录名必须映射到用户的成员`db_owner`中的固定的数据库角色**分发**数据库。  
  
7.  重复步骤 1 至 4，为本地 repl_merge 帐户创建登录名。 此登录名必须在 **distribution** 数据库和 **AdventureWorks** 数据库中拥有用户映射。  
  
## <a name="see-also"></a>请参阅  
 [“配置分发”](configure-distribution.md)   
 [Replication Agent Security Model](security/replication-agent-security-model.md)  
  
  