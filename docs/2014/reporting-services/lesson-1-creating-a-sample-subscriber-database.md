---
title: 第 1 课：创建示例订阅服务器数据库 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9e68650b21ee8cddc6258ab64b874bcf51ec1a83
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108539"
---
# <a name="lesson-1-creating-a-sample-subscriber-database"></a>第 1 课：创建示例订阅服务器数据库
  定义数据驱动的订阅前，必须具有可提供订阅数据的数据源。 在此步骤中，您将创建一个小型数据库，以存储本教程中使用的订阅数据。 稍后在处理订阅时，报表服务器将检索此数据并使用它来自定义报表输出、传递选项和报表表示格式。  
  
 本课程假定您使用[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]若要创建[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]数据库。  
  
### <a name="to-create-a-sample-subscriber-database"></a>创建示例订阅服务器数据库  
  
1.  启动 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]，打开到[!INCLUDE[ssDE](../includes/ssde-md.md)]的连接。  
  
2.  右键单击“数据库”，选择“新建数据库”。  
  
3.  在新的数据库对话框中的数据库名称中，键入*订户*。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  在工具栏中，单击“新建查询”按钮。  
  
5.  将下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句复制到空查询中：  
  
    ```  
    Use Subscribers  
    CREATE TABLE [dbo].[OrderInfo] (  
        [SubscriptionID] [int] NOT NULL PRIMARY KEY ,  
        [Order] [nvarchar] (20) NOT NULL,  
        [FileType] [bit],  
        [Format] [nvarchar] (20) NOT NULL ,  
    ) ON [PRIMARY]  
    GO  
  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('1', 'so43659', '1', 'IMAGE')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('2', 'so43664', '1', 'MHTML')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('3', 'so43668', '1', 'PDF')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('4', 'so71949', '1', 'Excel')  
    GO  
    ```  
  
6.  单击 **！在工具栏上执行** 。  
  
7.  使用 SELECT 语句查看您是否有三行数据。 例如： `select * from OrderInfo`  
  
## <a name="next-steps"></a>后续步骤  
 您已成功创建了订阅数据，这些数据将为每个订阅服务器驱动报表分发并改变报表输出。 下一步，将修改要分发给订阅服务器的报表的数据源属性。 修改数据源属性是为了准备报表以实现数据驱动的订阅传递。 您还将修改报表设计以便包括订阅将用于订阅服务器数据的参数。 [第 2 课：修改报表数据源属性](lesson-2-modifying-the-report-data-source-properties.md)。  
  
## <a name="see-also"></a>请参阅  
 [创建数据驱动订阅（SSRS 教程）](create-a-data-driven-subscription-ssrs-tutorial.md)   
 [创建数据库](../relational-databases/databases/create-a-database.md)   
 [创建基本表报表（SSRS 教程）](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
