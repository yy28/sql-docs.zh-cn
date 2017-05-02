---
title: "第 2 课：创建合并发布订阅 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 06722baa-9065-443e-b1d5-99036cf89074
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 423ad3b42e75c70e6826e04a298c5eac4e590291
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-2-creating-a-subscription-to-the-merge-publication"></a>第 2 课：创建合并发布订阅
在本课中，将使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]创建订阅。 然后，为订阅数据库设置权限，并手动生成新订阅的筛选数据快照。 本课程要求已完成上一课， [第 1 课：使用合并复制发布数据](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)。  
  
### <a name="to-create-the-subscription"></a>创建订阅  
  
1.  连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的订阅服务器，依次展开服务器节点和“复制”****文件夹，右键单击“本地订阅”****文件夹，然后单击“新建订阅”****。  
  
    新建订阅向导将启动。  
  
2.  在“发布”****页上，单击“发布服务器”****列表中的“查找 SQL Server 发布服务器”****。  
  
3.  在“连接到服务器”****对话框的“服务器名称”****框中，输入发布服务器实例的名称，然后单击“连接”****。  
  
4.  单击“AdvWorksSalesOrdersMerge”****，然后单击“下一步”****。  
  
5.  在“合并代理位置”页上，单击“在其订阅服务器上运行每个代理”****，然后单击“下一步”****。  
  
6.  在“订阅服务器”页上，选择订阅服务器的实例名称，然后在“订阅数据库”****下，从列表中选择“<New Database>”****。  
  
7.  在“新建数据库”****对话框的“数据库名称”****框中输入 **SalesOrdersReplica**，然后依次单击“确定”****和“下一步”****。  
  
8.  在“合并代理安全性”页上，单击省略号 (**…**) 按钮，在“进程帐户”****框中输入 \<*Machine_Name>***\repl_merge**，为此帐户提供密码，依次单击“确定”****和“下一步”****，然后再次单击“下一步”****。  
  
9. 在“初始化订阅”页上，从“初始化时间”****列表中选择“首次同步时”****，单击“下一步”****，然后再次单击“下一步”****。  
  
10. 在“HOST_NAME 值”页的“HOST_NAME 值”****框中，输入值 **adventure-works\pamela0**，然后单击“完成”****。  
  
11. 再次单击“完成”****，创建订阅后，单击“关闭”****。  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>在订阅服务器上设置数据库权限  
  
1.  连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的订阅服务器，依次展开“数据库”****、“SalesOrdersReplica”****和“安全性”****，右键单击“用户”****，然后选择“新建用户”****。  
  
2.  在“常规”****页的“用户名”****框中输入 \<*Machine_Name>***\repl_merge**，然后依次单击省略号 (**…**) 按钮和“浏览”****，选择 \<*Machine_Name>***\repl_merge**，然后依次单击“确定”****、“检查名称”****和“确定”****。  
  
3.  在“数据库角色成员资格”****中，选择“db_owner”****，然后单击“确定”****以创建用户。  
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>创建订阅的筛选数据快照  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”****文件夹。  
  
2.  在“本地发布”****文件夹中，右键单击“AdvWorksSalesOrdersMerge”****发布，然后单击“属性”****。  
  
    将显示“发布属性”****对话框。  
  
3.  选择“数据分区”****页，然后单击“添加”****。  
  
4.  在“添加数据分区”****对话框的“HOST_NAME 值”****框中，键入 **adventure-works\pamela0**，然后单击“确定”****。  
  
5.  选择新添加的分区，单击“立即生成所选快照”****，然后单击“确定”****。  
  
## <a name="next-steps"></a>后续步骤  
您已经成功地对合并发布创建了一个订阅，并且为该新订阅的数据分区生成了筛选快照，因此初始化订阅后即可使用此筛选快照。 接下来，您将对订阅数据库的合并代理授予权限，并且运行合并代理来启动订阅的同步和初始化操作。 请参阅 [第 3 课：使订阅与合并发布同步](../../relational-databases/replication/lesson-3-synchronizing-the-subscription-to-the-merge-publication.md)。  
  
## <a name="see-also"></a>另请参阅  
[订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
[创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)  
[带有参数化筛选器的合并发布的快照](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  

