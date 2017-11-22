---
title: "创建系统版本控制的内存优化临时表 | Microsoft Docs"
ms.custom: 
ms.date: 05/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c1fc682-bf5b-4096-a0ff-3235d71c205a
caps.latest.revision: "14"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bdbc79848f6484ccf4638d29b1e09221e7ca6e36
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="creating-a-memory-optimized-system-versioned-temporal-table"></a>创建系统版本控制的内存优化临时表
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  与创建基于磁盘的历史记录表类似，你可以通过多种方式创建内存优化的临时表。  
  
> [!NOTE]  
>  若要创建内存优化表，必须首先创建 [内存优化的文件组](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)。  
  
 如果想要控制命名并仍依赖于系统创建具有默认配置的历史记录表，使用默认历史记录表创建临时表是一个方便的选项。 在下面的示例中，新系统版本控制的内存优化临时表链接到新的基于磁盘的历史记录表。  
  
```  
CREATE SCHEMA History  
GO  
CREATE TABLE dbo.Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH   
    (  
        MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,  
            SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )   
    );  
```  
  
 当希望使用现有表添加系统版本控制时（如当你希望将自定义临时解决方案迁移到内置支持时），创建链接到现有历史记录表的临时表是非常有用的。 在下面的示例中，创建了链接到现有历史记录表的新临时表。  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (  
        SYSTEM_VERSIONING = ON  
            (  
                HISTORY_TABLE = dbo.Department_History  
                , DATA_CONSISTENCY_CHECK = ON   
            )  
        , MEMORY_OPTIMIZED = ON  
        , DURABILITY = SCHEMA_AND_DATA  
    );  
```  
  
## <a name="did-this-article-help-you-were-listening"></a>本文是否对你有帮助？ 我们洗耳恭听  
 你正在查找哪些信息，是否已经找到？ 我们不断听取你的反馈来改进内容。 请将你的评论提交到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Creating%20a%20Memory-Optimized%20System-Versioned%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>另请参阅  
 [系统版本控制临时表与内存优化表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [使用带有系统版本的内存优化临时表](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [监视系统版本控制型内存优化临时表](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [内存优化系统版本控制临时表的性能注意事项](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [临时表](../../relational-databases/tables/temporal-tables.md)   
 [临时表系统一致性检查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [管理版本由系统控制的临时表中历史数据的保留期](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [临时表元数据视图和函数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
