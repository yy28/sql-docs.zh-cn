---
title: 分区存储模式和处理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- hybrid OLAP
- data storage [Analysis Services]
- relational OLAP
- multidimensional OLAP
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- HOLAP
- MOLAP
- ROLAP
ms.assetid: 86d17547-a0b6-47ac-876c-d7a5b15ac327
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74f53ddb6e7e3fc6b9d14ddcc726c2766a598860
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727573"
---
# <a name="partition-storage-modes-and-processing"></a>分区存储模式和处理
  分区的存储模式影响分区及其父度量值组和多维数据集的查询和处理性能、存储要求以及存储位置。 存储模式的选择也会影响处理选择。  
  
 分区可以使用下列三种基本存储模式之一：  
  
-   多维 OLAP (MOLAP)  
  
-   关系 OLAP (ROLAP)  
  
-   混合 OLAP (HOLAP)  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持所有三种基本存储模式。 它还支持主动缓存，使用主动缓存，您可以组合 ROLAP 和 MOLAP 存储的特征，从而满足数据的即时性和查询性能的要求。 有关详细信息，请参阅[主动缓存（分区）](partitions-proactive-caching.md)。  
  
## <a name="molap"></a>MOLAP  
 在 MOLAP 存储模式下，处理分区时，分区的聚合及其源数据副本将存储在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 内的多维结构中。 此 MOLAP 结构在得到高度优化后，可以最大程度地提高查询性能。 该存储位置可以位于用来定义分区的计算机上，也可以位于其他运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的计算机上。 由于源数据副本位于多维结构中，因此，可以在不访问分区源数据的情况下直接解析查询。 使用聚合可以显著缩短查询响应时间。 分区 MOLAP 结构中的数据与分区的最新处理完全保持同步。  
  
 随着源数据的更改，MOLAP 存储中的对象必须定期处理以合并这些更改并使其可供用户使用。 处理会完全更新或增量更新 MOLAP 结构中的数据。 两次处理之间的时间将构成滞后时间，在此期间，OLAP 对象中的数据可能无法与源数据相匹配。 您可以增量更新或完全更新 MOLAP 存储中的对象，而无需使分区或多维数据集脱机。 但是，在某些情况下可能需要使多维数据集脱机以处理对 OLAP 对象所做的特定结构更改。 您可以通过更新和处理临时服务器上的多维数据集以及使用数据库同步将已处理的对象复制到生成服务器，最小化更新 MOLAP 存储所需的中断时间。 还可以使用主动缓存，在保留 MOLAP 存储的大多数性能优点的同时最小化滞后时间，并最大化可用性。 有关详细信息，请参阅[主动缓存&#40;分区&#41;](partitions-proactive-caching.md)，[同步 Analysis Services 数据库](../multidimensional-models/synchronize-analysis-services-databases.md)，并且[多维模型对象处理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="rolap"></a>ROLAP  
 在 ROLAP 存储模式下，分区的聚合将存储在关系数据库（在分区数据源中指定）的索引视图中。 与 MOLAP 存储模式不同，ROLAP 不会将源数据的副本存储到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据文件夹中。 当不能从查询缓存中获得结果时，则会访问数据源中的索引视图以回答查询。 使用 ROLAP 存储的查询响应速度通常比使用 MOLAP 或 HOLAP 存储模式更慢。 使用 ROLAP 时的处理时间通常也较长。 但是，使用不经常执行查询的大型数据集（例如纯粹的历史记录数据）时，用户可以使用 ROLAP 实时查看数据并可节省存储空间。  
  
> [!NOTE]  
>  使用 ROLAP 时，如果联接与 GROUP BY 子句结合使用，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可能返回与未知成员相关的不正确信息。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将消除相关的完整性错误，而不是返回未知成员值。  
  
 如果分区使用 ROLAP 存储模式并且其源数据存储在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将试图创建索引视图以包含分区的聚合。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 无法创建索引视图，便也无法创建聚合表。 尽管 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会处理在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 上创建索引视图的会话要求，但 ROLAP 分区及其架构中的表必须满足以下条件才能让 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 为聚合创建索引视图：  
  
-   分区不能包含使用 `Min` 或 `Max` 聚合函数的度量值。  
  
-   ROLAP 分区架构中的每个表必须只能使用一次。 例如，架构不能包含 [dbo].[address] AS "Customer Address" 和 [dbo].[address] AS "SalesRep Address"。  
  
-   每个表都必须是表而不是视图。  
  
-   分区架构中的所有表名都必须由所有者名称限定，例如 [dbo].[customer]。  
  
-   分区架构内的所有表都必须有相同的所有者；例如，所使用的 FROM 子句不能引用表 [tk].[customer]、[john].[store] 和 [dave].[sales_fact_2004]。  
  
-   分区度量值的源列不能为空。  
  
-   视图中使用的所有表在创建时都必须将下列选项设置为 ON：  
  
    -   ANSI_NULLS  
  
    -   QUOTED_IDENTIFIER  
  
-   在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中，索引键的总计大小不能超过 900 字节。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 将断定此条件基于固定的长度键列，则在处理 CREATE INDEX 语句时。 但是，如果索引键中有可变长度列[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]断定此条件的基表的每个更新。 因为不同的聚合具有不同的视图定义，所以使用索引视图的 ROLAP 处理可能成功，也可能失败，具体取决于聚合设计。  
  
-   创建索引的视图的会话必须具有以下选项设置为 ON:ARITHABORT、 CONCAT_NULL_YEILDS_NULL、 QUOTED_IDENTIFIER、 ANSI_NULLS、 ANSI_PADDING 和 ANSI_WARNING。 可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中对此进行设置。  
  
-   创建索引的视图的会话必须具有以下选项设置为 OFF:NUMERIC_ROUNDABORT。 可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中对此进行设置。  
  
## <a name="holap"></a>HOLAP  
 HOLAP 存储模式结合了 MOLAP 和 ROLAP 二者的特性。 同 MOLAP 一样，在 holap 下分区存储在多维结构中的聚合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例。 HOLAP 不会使源数据的副本存储起来。 就只访问分区聚合中的汇总数据的查询而言，HOLAP 与 MOLAP 相同。 访问源数据的查询-例如，如果你想要深化到原子多维数据集单元格它们没有任何聚合数据必须从关系数据库检索数据并不会将如果源数据存储在 MOLAP structur 尽可能快地e。 在 HOLAP 存储模式下，通常用户执行各查询所用的时间明显不同，具体取决于是根据缓存或聚合解析查询还是根据源数据本身解析查询。  
  
 按 HOLAP 存储的分区小于相应按 MOLAP 存储的分区（因为前者不包含源数据），而比 ROLAP 分区响应涉及汇总数据的查询要快。 一般情况下，HOLAP 存储模式适用于多维数据集中要求快速响应基于大量源数据的汇总的查询的分区。 但是，当用户生成必须涉及叶级数据的查询时（例如，计算中值），通常最好选择 MOLAP。  
  
## <a name="see-also"></a>请参阅  
 [主动缓存&#40;分区&#41;](partitions-proactive-caching.md)   
 [同步 Analysis Services 数据库](../multidimensional-models/synchronize-analysis-services-databases.md)   
 [分区（Analysis Services - 多维数据）](partitions-analysis-services-multidimensional-data.md)  
  
  
