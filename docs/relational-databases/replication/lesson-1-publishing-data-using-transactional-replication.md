---
title: "第 1 课：使用事务复制发布数据 | Microsoft Docs"
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
ms.assetid: 9c55aa3c-4664-41fc-943f-e817c31aad5e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 021ff6838de18ea03a50aae661d543061088ae87
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-1-publishing-data-using-transactional-replication"></a>第 1 课：使用事务复制发布数据
在本课中，使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建一个事务发布，以便在 **示例数据库中发布** Product [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 表的筛选子集。 您还要将分发代理使用的 SQL Server 登录名添加到发布访问列表 (PAL)。 开始本教程之前，应已完成上一个教程 [准备用于复制的服务器](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)。  
  
### <a name="to-create-a-publication-and-define-articles"></a>创建发布和定义项目  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开“复制”文件夹，右键单击“本地发布”文件夹，再单击“新建发布”。  
  
    将启动发布配置向导。  
  
3.  在“发布数据库”页上，选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然后单击“下一步”。  
  
4.  在“发布类型”页上，选择“事务发布”，然后单击“下一步”。  
  
5.  在“项目”页上，展开“表”节点，选中“Product”复选框，然后展开“Product”并取消选中“ListPrice”和“StandardCost”复选框。 单击“下一步” 。  
  
6.  在“筛选表行”页上，单击“添加”。  
  
7.  在“添加筛选器”对话框中，单击 **SafetyStockLevel** 列，再单击向右箭头以将此列添加到筛选查询的筛选语句的 WHERE 子句，并修改 WHERE 子句，如下所示：  
  
    ```  
    WHERE [SafetyStockLevel] < 500  
    ```  
  
8.  单击“确定”，然后单击“下一步”。  
  
9. 选中“立即创建快照并使快照保持可用状态，以初始化订阅”复选框，单击“下一步”。  
  
10. 在“代理安全性”页上，清除“使用快照代理的安全设置”复选框。  
  
11. 单击快照代理的“安全设置”，在“进程帐户”框中输入 \<*Machine_Name>***\repl_snapshot**，为此帐户提供密码，然后单击“确定”。  
  
12. 重复上一步，将 repl_logreader 设置为日志读取器代理的进程帐户，然后单击“完成”。  
  
13. 在“完成向导”页的“发布名称”框中，键入 **AdvWorksProductTrans**，然后单击“完成”。  
  
14. 创建发布后，单击“关闭”完成该向导。  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>查看快照的生成状态  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。  
  
2.  在“本地发布”文件夹中，右键单击 **AdvWorksProductTrans**，再单击“查看快照代理状态”。  
  
3.  将显示该发布的快照代理作业的当前状态。 继续下一课之前，请确保快照作业已成功完成。  
  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>将分发代理登录名添加到 PAL  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。  
  
2.  在“本地发布”文件夹中，右键单击 **AdvWorksProductTrans**，再单击“属性”。  
  
    将显示“发布属性”对话框。  
  
3.  选择“发布访问列表”页，单击“添加”。  
  
4.  \在“添加发布访问项”对话框中，选择 *<Machine_Name>***\repl_distribution**，再单击“确定”。 单击 **“确定”**。  
  
## <a name="next-steps"></a>后续步骤  
您已成功创建了事务发布。 接下来，您将订阅此发布。 请参阅 [第 2 课：创建事务发布的订阅](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md)。  
  
## <a name="see-also"></a>另请参阅  
[筛选已发布数据](../../relational-databases/replication/publish/filter-published-data.md)  
[定义项目](../../relational-databases/replication/publish/define-an-article.md)  
[创建并应用快照](../../relational-databases/replication/create-and-apply-the-snapshot.md)  
  
  
  

