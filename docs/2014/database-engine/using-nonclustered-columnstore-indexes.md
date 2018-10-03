---
title: 使用非聚集列存储索引 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 4c341fb8-7cb1-4cab-921b-e80b751d6c19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e97aed3a5a4f5b49e482479b58928d2092a314f9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182490"
---
# <a name="using-nonclustered-columnstore-indexes"></a>使用非聚集列存储索引
  描述用于在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 表上使用非聚集列存储索引的主要任务。  
  
 有关列存储索引的概述，请参阅[列存储索引介绍](../relational-databases/indexes/columnstore-indexes-described.md)。  
  
 有关聚集列存储索引的信息，请参阅[使用聚集列存储索引](../relational-databases/indexes/indexes.md)。  
  
## <a name="contents"></a>目录  
  
-   [创建非聚集列存储索引](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#load)  
  
-   [更改非聚集列存储索引中的数据](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#change)  
  
##  <a name="load"></a> 创建非聚集列存储索引  
 将数据加载到聚集列存储索引，第一个将数据加载到传统行存储表存储为堆或聚集索引，以及如何将[创建列存储索引&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql)若要创建列存储索引。  
  
 ![数据加载到列存储索引](../../2014/database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "数据加载到列存储索引")  
  
##  <a name="change"></a> 更改非聚集列存储索引中的数据  
 在您在表上创建非聚集列存储索引后，不能直接在该表中修改数据。 具有 INSERT、UPDATE、DELETE 或 MERGE 的查询将失败并且返回错误消息。 若要添加或修改表中的数据，可以执行以下操作之一：  
  
-   禁用列存储索引。 然后可以更新表中的数据。 如果禁用列存储索引，则可以在完成数据更新后重新生成列存储索引。 例如：  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   删除列存储索引，更新表，然后重新创建列存储索引，创建列存储索引。 例如：  
  
    ```  
    DROP INDEX mycolumnstoreindex ON mytable  
    -- update mytable --  
    CREATE NONCLUSTERED COLUMNSTORE INDEX mycolumnstoreindex ON mytable;  
  
    ```  
  
-   将数据加载到不含列存储索引的临时表中。 在临时表上生成列存储索引。 将临时表切换到主表的一个空分区中。  
  
-   将分区从具有列存储索引的表切换到一个空的临时表中。 如果在临时表上有某个列存储索引，则禁用该列存储索引。 执行任何更新。 生成（或重新生成）列存储索引。 将临时表切换回主表的（现在为空的）分区中。  
  

  
  
