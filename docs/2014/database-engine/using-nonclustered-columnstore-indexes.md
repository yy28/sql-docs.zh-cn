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
ms.openlocfilehash: c190e95df57c80d29428b39b72a4115ac7d23de1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175346"
---
# <a name="using-nonclustered-columnstore-indexes"></a>使用非聚集列存储索引
  描述用于在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 表上使用非聚集列存储索引的主要任务。

 有关列存储索引的概述，请参阅 [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md)。

 有关聚集列存储索引的信息，请参阅 [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md)。

## <a name="contents"></a>目录

-   [创建非聚集列存储索引](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#load)

-   [更改非聚集列存储索引中的数据](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#change)

##  <a name="create-a-nonclustered-columnstore-index"></a><a name="load"></a>创建非聚集列存储索引
 若要将数据加载到非聚集列存储索引中，请首先将数据加载到作为堆或聚集索引存储的传统行存储表中，然后使用[CREATE 列存储索引 &#40;transact-sql&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)创建列存储索引。

 ![将数据加载到列存储索引中](../../2014/database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "将数据加载到列存储索引中")

##  <a name="change-the-data-in-a-nonclustered-columnstore-index"></a><a name="change"></a>更改非聚集列存储索引中的数据
 在您在表上创建非聚集列存储索引后，不能直接在该表中修改数据。 具有 INSERT、UPDATE、DELETE 或 MERGE 的查询将失败并且返回错误消息。 若要添加或修改表中的数据，可以执行以下操作之一：

-   禁用列存储索引。 然后可以更新表中的数据。 如果禁用列存储索引，则可以在完成数据更新后重新生成列存储索引。 例如：

    ```
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;
    -- update mytable --
    ALTER INDEX mycolumnstoreindex on mytable REBUILD
    ```

-   删除列存储索引，更新表，然后重新创建包含 CREATE 列存储索引的列存储索引。 例如：

    ```
    DROP INDEX mycolumnstoreindex ON mytable
    -- update mytable --
    CREATE NONCLUSTERED COLUMNSTORE INDEX mycolumnstoreindex ON mytable;

    ```

-   将数据加载到不含列存储索引的临时表中。 在临时表上生成列存储索引。 将临时表切换到主表的一个空分区中。

-   将分区从具有列存储索引的表切换到一个空的临时表中。 如果在临时表上有某个列存储索引，则禁用该列存储索引。 执行任何更新。 生成（或重新生成）列存储索引。 将临时表切换回主表的（现在为空的）分区中。




