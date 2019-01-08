---
title: 发布属性 - 数据分区 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.datapartitions.f1
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 91a11856c8cde6ed94ce2a954ae51c58e4aabf7f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52752259"
---
# <a name="publication-properties-data-partitions"></a>发布属性，数据分区
  可以使用 **“发布属性”** 对话框的 **“数据分区”** 页，定义使用参数化筛选的合并发布的数据分区。 在定义分区后，您随后还可以生成这些分区的快照，为基于订阅服务器的连接属性（登录名和/或计算机名称）的不同订阅服务器提供不同的初始数据集。 如果订阅服务器在第一次同步时对其分区没有可用的快照，您还可以选择允许订阅服务器请求快照的传递和生成。 有关详细信息，请参阅 [为包含参数化筛选器的合并发布创建快照](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
## <a name="options"></a>选项  
 **添加**  
 单击 **“添加”** 可以定义分区。 在 **“添加数据分区”** 对话框中，为 **HOST_NAME()** 和/或 **SUSER_SNAME()** 指定值，再定义计划以刷新快照即可。  
  
 **编辑**  
 选择网格中的现有分区，再单击 **“编辑”** 可以编辑相应的分区。  
  
 **删除**  
 选择网格中的现有分区，再单击 **“删除”** 可以删除相应的分区。  
  
 **立即生成所选快照**  
 选择网格中的一个或多个分区，再单击 **“立即生成所选快照”** 可以生成这些分区的快照。  
  
 **清除现有快照**  
 选择网格中的一个或多个分区，再单击 **“清除现有快照”** 可以清除这些分区的快照。  
  
 **在新订阅服务器尝试同步时，根据需要自动定义分区并生成快照**  
 如果希望允许订阅服务器请求快照的生成和应用程序，请选择此选项。 如果订阅服务器在第一次同步时对其分区没有可用的快照，则订阅服务器可能要求设置此选项。  
  
## <a name="see-also"></a>请参阅  
 [Create a Publication](publish/create-a-publication.md)   
 [查看和修改发布属性](publish/view-and-modify-publication-properties.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [发布数据和数据库对象](publish/publish-data-and-database-objects.md)   
 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
