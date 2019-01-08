---
title: 第 2 课：创建对合并发布的订阅 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 06722baa-9065-443e-b1d5-99036cf89074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 8634606ba3eaba8a38aefb66043c0d00e33660a2
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590991"
---
# <a name="lesson-2-creating-a-subscription-to-the-merge-publication"></a>第 2 课：创建合并发布的订阅
  在本课中，将使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]创建订阅。 然后，为订阅数据库设置权限，并手动生成新订阅的筛选数据快照。 本课程要求已完成上一课，[第 1 课：使用合并复制发布数据](lesson-1-publishing-data-using-merge-replication.md)。  
  
### <a name="to-create-the-subscription"></a>创建订阅  
  
1.  连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的订阅服务器，依次展开服务器节点和“复制”文件夹，右键单击“本地订阅”文件夹，然后单击“新建订阅”。  
  
     新建订阅向导将启动。  
  
2.  在“发布”页上，单击“发布服务器”列表中的“查找 SQL Server 发布服务器”。  
  
3.  在“连接到服务器”对话框的“服务器名称”框中，输入发布服务器实例的名称，然后单击“连接”。  
  
4.  单击“AdvWorksSalesOrdersMerge”，然后单击“下一步”。  
  
5.  在“合并代理位置”页上，单击“在其订阅服务器上运行每个代理”，然后单击“下一步”。  
  
6.  在订阅服务器页上，选择的实例名称的订阅服务器，并在**订阅数据库**，选择**\<新数据库 >** 从列表中。  
  
7.  在“新建数据库”对话框的“数据库名称”框中输入 **SalesOrdersReplica**，然后依次单击“确定”和“下一步”。  
  
8.  在合并代理安全性页上，单击旁边的省略号 (**...**) 按钮，输入\< _m a c h >_**\repl_merge**中**进程帐户**框中，为此帐户提供密码，单击**确定**，单击**下一步**，然后单击**下一步**试。  
  
9. 在“初始化订阅”页上，从“初始化时间”列表中选择“首次同步时”，单击“下一步”，然后再次单击“下一步”。  
  
10. 在 HOST_NAME 值页上，输入值`adventure-works\pamela0`中**HOST_NAME 值**框中，然后依次**完成**。  
  
11. 再次单击“完成”，创建订阅后，单击“关闭”。  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>在订阅服务器上设置数据库权限  
  
1.  连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的订阅服务器，依次展开“数据库”、“SalesOrdersReplica”和“安全性”，右键单击“用户”，然后选择“新建用户”。  
  
2.  上**常规**页上，输入\< _m a c h >_**\repl_merge**中**用户名**框中，单击省略号 （**...**) 按钮，再单击**浏览**，选择\< _m a c h >_**\repl_merge**，单击**确定**，单击**检查名称**，然后单击**确定**。  
  
3.  在“数据库角色成员资格”中，选择“db_owner”，然后单击“确定”以创建用户。  
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>创建订阅的筛选数据快照  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。  
  
2.  在“本地发布”文件夹中，右键单击“AdvWorksSalesOrdersMerge”发布，然后单击“属性”。  
  
     将显示“发布属性”对话框。  
  
3.  选择“数据分区”页，然后单击“添加”。  
  
4.  在中**添加数据分区**对话框中，键入`adventure-works\pamela0`中**HOST_NAME 值**框中，然后依次**确定**。  
  
5.  选择新添加的分区，单击“立即生成所选快照”，然后单击“确定”。  
  
## <a name="next-steps"></a>后续步骤  
 您已经成功地对合并发布创建了一个订阅，并且为该新订阅的数据分区生成了筛选快照，因此初始化订阅后即可使用此筛选快照。 接下来，您将对订阅数据库的合并代理授予权限，并且运行合并代理来启动订阅的同步和初始化操作。 请参阅[第 3 课：同步对合并发布的订阅](lesson-3-synchronizing-the-subscription-to-the-merge-publication.md)。  
  
## <a name="see-also"></a>请参阅  
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
