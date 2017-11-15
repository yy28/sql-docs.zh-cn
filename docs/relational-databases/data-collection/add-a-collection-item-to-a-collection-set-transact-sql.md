---
title: "将收集项添加到收集组中 (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collection items [SQL Server]
- collection sets [SQL Server], adding items
ms.assetid: 9fe6454e-8c0e-4b50-937b-d9871b20fd13
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 08104faa0f62ace56b291bc6fa45290e826b773b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="add-a-collection-item-to-a-collection-set-transact-sql"></a>将收集项添加到收集组中 (Transact-SQL)
  可以使用随数据收集器一起提供的存储过程将收集项添加到现有收集组中。  
  
 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的查询编辑器执行以下步骤。  
  
### <a name="add-a-collection-item-to-a-collection-set"></a>将收集项添加到收集组中  
  
1.  通过运行 **sp_syscollector_stop_collection_set** 存储过程停止要向其中添加收集项的收集组。 例如，若要停止名为“Test Collection Set”的收集组，请运行下列语句：  
  
    ```tsql  
    USE msdb  
    DECLARE @csid int  
    SELECT @csid = collection_set_id  
    FROM syscollector_collection_sets  
    WHERE name = 'Test Collection Set'  
    SELECT @csid  
    EXEC dbo.sp_syscollector_stop_collection_set @collection_set_id = @csid  
    ```  
  
    > [!NOTE]  
    >  还可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的对象资源管理器来停止收集组。 有关详细信息，请参阅 [启动或停止收集组](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)。  
  
2.  声明要向其中添加收集项的收集组。 下面的代码提供了一个演示如何声明收集组 ID 的示例。  
  
    ```tsql  
    DECLARE @collection_set_id_1 int  
    SELECT @collection_set_id_1 = collection_set_id FROM [msdb].[dbo].[syscollector_collection_sets]  
    WHERE name = N'Test Collection Set'; -- name of collection set  
    ```  
  
3.  声明收集器类型。 下面的代码提供了一个演示如何声明一般 T-SQL 查询收集器类型的示例。  
  
    ```tsql  
    DECLARE @collector_type_uid_1 uniqueidentifier  
    SELECT @collector_type_uid_1 = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
       WHERE name = N'Generic T-SQL Query Collector Type';  
    ```  
  
     可以运行下面的代码以获取已安装收集器类型的列表：  
  
    ```tsql  
    USE msdb  
    SELECT * from syscollector_collector_types  
    GO  
    ```  
  
4.  运行 **sp_syscollector_create_collection_item** 存储过程来创建收集项。 必须声明收集项的架构，以便它映射到所需收集器类型要求的架构。 下面的示例使用一般 T-SQL 查询输入架构。  
  
    ```tsql  
    DECLARE @collection_item_id int;  
    EXEC [msdb].[dbo].[sp_syscollector_create_collection_item]   
    @name=N'OS Wait Stats', --name of collection item  
    @parameters=N'  
    <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
     <Query>  
      <Value>select * from sys.dm_os_wait_stats</Value>  
      <OutputTable>os_wait_stats</OutputTable>  
    </Query>  
    </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 60,  
    @collection_set_id = @collection_set_id_1, --- Provides the collection set ID number  
    @collector_type_uid = @collector_type_uid_1 -- Provides the collector type UID  
    SELECT @collection_item_id     
    ```  
  
5.  在启动已更新的收集组之前，运行以下查询来验证新的收集项是否已创建：  
  
    ```xaml  
    USE msdb  
    SELECT * from syscollector_collection_sets  
    SELECT * from syscollector_collection_items  
    GO  
    ```  
  
     收集组和它们的收集项都显示在 **“结果”** 选项卡中。  
  
## <a name="see-also"></a>另请参阅  
 [创建使用一般 T-SQL 查询收集器类型的自定义收集组 (Transact-SQL)](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
