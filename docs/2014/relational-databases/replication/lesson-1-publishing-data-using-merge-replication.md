---
title: 第 1 课：使用合并复制发布数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: c3c6e0b6-54cd-4b7d-8efb-2cefe14fcd7f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 65debc2ad15045984f43e05d0afcf3011c50f2b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112907"
---
# <a name="lesson-1-publishing-data-using-merge-replication"></a>第 1 课：使用合并复制发布数据
  在本课中，你将使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建合并复制以在 **示例数据库中发布**Employee **、** SalesOrderHeader **和** SalesOrderDetail [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 表的子集。 这些表用参数化行筛选器进行筛选，以便每个订阅都包含唯一的数据分区。 你还要将合并代理使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名添加到发布访问列表 (PAL) 中。 本教程要求你完成上一个教程， [准备用于复制的服务器](tutorial-preparing-the-server-for-replication.md)的学习。  
  
### <a name="to-create-a-publication-and-define-articles"></a>创建发布和定义项目  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开“复制”文件夹，右键单击“本地发布”，再单击“新建发布”。  
  
     将启动发布配置向导。  
  
3.  在“发布数据库”页上，选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然后单击“下一步”。  
  
4.  在“发布类型”页上，选择“合并发布”，然后单击“下一步”。  
  
5.  在“订阅服务器类型”页上，确保仅选中了 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本，然后单击“下一步”。  
  
6.  在“项目”页上，展开“表”节点，选择“SalesOrderHeader”和“SalesOrderDetail”，然后展开“Employee”，选择“EmployeeID”或“LoginID”，然后单击“下一步”。  
  
    > [!TIP]  
    >  将自动选择所需的其他列。 选择任一自动选择的列并查看“要发布的对象”列表下有关解释列为必需的原因的说明。  
  
7.  在“筛选表行”页上，单击“添加”，然后单击“添加筛选器”。  
  
8.  在“添加筛选器”对话框的“选择要筛选的表”中，选择“Employee (HumanResources)”，单击“LoginID”列，再单击向右箭头以将此列添加到筛选查询的 WHERE 子句中，并将 WHERE 子句修改如下：  
  
    ```  
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
9. 单击“此表中的行将仅转到一个订阅”，再单击“确定”。  
  
10. 在“筛选表行”页上，单击“Employee (Human Resources)”，单击“添加”，然后单击“添加联接以扩展所选筛选器”。  
  
11. 在“添加联接”对话框的“联接的表”下，选择“Sales.SalesOrderHeader”，然后单击“手动编写联接语句”，将联接语句完成如下：  
  
    ```  
    ON Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
    ```  
  
12. 在“指定联接选项”中，选择“唯一键”，然后单击“确定”。  
  
13. 在“筛选表行”页上，单击“SalesOrderHeader”，再单击“添加”，然后单击“添加联接以扩展所选筛选器”。  
  
14. 在“添加联接”对话框的“联接的表”下，选择“Sales.SalesOrderDetail”。  
  
15. 单击“手动编写联接语句”。  
  
16. 在“筛选的表列”中，选择“BusinessEntityID”，然后单击箭头按钮将列名称复制到联接语句。  
  
17. 在“联接语句”框中，按如下所示完成联接语句：  
  
    ```  
    ON Employee.BusinessEntityID = SalesOrderHeader.SalesPersonID  
    ```  
  
18. 在“指定联接选项”中，选择“唯一键”，然后单击“确定”。  
  
19. 在“筛选表行”页上，单击“SalesOrderHeader (Sales)”，再单击“添加”，然后单击“添加联接以扩展所选筛选器”。  
  
20. 在“添加联接”对话框的“联接的表”下，选择“Sales.SalesOrderDetail”，单击“确定”，然后单击“下一步”。  
  
21. 选中“立即创建快照”，清除“计划在以下时间运行快照代理”，然后单击“下一步”。  
  
22. 在“代理安全性”页上，单击“安全设置”，在“进程帐户”框中键入 \<Machine_Name>\repl_snapshot，为此帐户提供密码，然后单击“确定”。 单击 **“完成”**。  
  
23. 在“完成该向导”页的“发布名称”框中，输入 **AdvWorksSalesOrdersMerge**，然后单击“完成”。  
  
24. 创建发布后，单击“关闭”。  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>查看快照的生成状态  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。  
  
2.  在“本地发布”文件夹中，右键单击 **AdvWorksSalesOrdersMerge**，再单击“查看快照代理状态”。  
  
3.  将显示该发布的快照代理作业的当前状态。 继续下一课之前，请确保快照作业已成功完成。  
  
### <a name="to-add-the-merge-agent-login-to-the-pal"></a>将合并代理登录名添加到 PAL  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。  
  
2.  在“本地发布”文件夹中，右键单击 **AdvWorksSalesOrdersMerge**，再单击“属性”。  
  
     将显示“发布属性”对话框。  
  
3.  选择“发布访问列表”页，单击“添加”。  
  
4.  在“添加发布访问项”对话框中，选择“<Machine_Name>\repl_merge”，然后单击“确定”。 单击“确定” 。  
  
## <a name="next-steps"></a>后续步骤  
 您已成功创建了合并发布。 接下来，您将订阅此发布。 请参阅 [第 2 课：创建合并发布订阅](lesson-2-creating-a-subscription-to-the-merge-publication.md)。  
  
## <a name="see-also"></a>请参阅  
 [筛选已发布数据](publish/filter-published-data.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [定义项目](publish/define-an-article.md)  
  
  
