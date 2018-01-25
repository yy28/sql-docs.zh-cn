---
title: "在事务发布中发布存储过程的执行 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 475af0dd026d8e3f5820e1678f4033856af2b0b5
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="publish-execution-of-stored-procedure-in-transactional-publication"></a>在事务发布中发布存储过程的执行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]可以在“项目属性 - \<项目>”对话框中指定应发布存储过程执行情况（而不仅仅是其定义）。 新建发布向导和“发布属性 - \<发布>”对话框中提供了该对话框。 有关使用该向导和访问该对话框的详细信息，请参阅[创建发布](../../../relational-databases/replication/publish/create-a-publication.md)以及[查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
 初始化订阅时，过程定义（CREATE PROCEDURE 语句）将被复制到订阅服务器上；当在发布服务器上执行过程时，复制将在订阅服务器上执行相应的过程。  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>发布存储过程的执行  
  
1.  在新建发布向导或“发布属性 - \<发布>”对话框的“项目”页上，选择一个存储过程。  
  
2.  单击 **“项目属性”**，然后单击 **“设置突出显示的存储过程项目的属性”**。  
  
3.  在“项目属性 - \<项目>”对话框中，为“复制”选项指定下面的一个值：  
  
    -   **存储过程的执行**  
  
    -   **SP 的序列化事务中的执行**  
  
         建议选择此选项，因为此选项仅当过程在可序列化事务的上下文中执行时才复制过程的执行。 如果存储过程在可序列化事务的外部执行，则已发布表中的数据更改将复制为一系列数据操作语言 (DML) 语句。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果处于“发布属性 - \<发布>”对话框中，请单击“确定”以保存并关闭该对话框。  
  
## <a name="see-also"></a>另请参阅  
 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
