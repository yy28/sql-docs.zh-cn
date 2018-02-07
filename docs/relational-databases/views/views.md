---
title: "视图 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: views
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- views [SQL Server], about views
ms.assetid: ada83c28-e8b7-45d9-b53c-b3d67c8820c8
caps.latest.revision: 
author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7ba650c638d855556ec2afe992f26ff3f6ad2460
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="views"></a>视图
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]
视图是一个虚拟表，其内容由查询定义。 同表一样，视图包含一系列带有名称的列和行数据。 视图在数据库中并不是以数据值存储集形式存在，除非是索引视图。 行和列数据来自由定义视图的查询所引用的表，并且在引用视图时动态生成。  
  
 对其中所引用的基础表来说，视图的作用类似于筛选。 定义视图的筛选可以来自当前或其他数据库的一个或多个表，或者其他视图。 分布式查询也可用于定义使用多个异类源数据的视图。 例如，如果有多台不同的服务器分别存储您的单位在不同地区的数据，而您需要将这些服务器上结构相似的数据组合起来，这种方式就很有用。  
  
 视图通常用来集中、简化和自定义每个用户对数据库的不同认识。 视图可用作安全机制，方法是允许用户通过视图访问数据，而不授予用户直接访问视图基础表的权限。 视图可用于提供向后兼容接口来模拟曾经存在但其架构已更改的表。 还可以在向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制数据和从其中复制数据时使用视图，以便提高性能并对数据进行分区。  
  
## <a name="types-of-views"></a>视图类型  
 除了基本用户定义视图的标准角色以外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还提供了下列类型的视图，这些视图在数据库中起着特殊的作用：  
  
 索引视图  
 索引视图是被具体化了的视图。 这意味着已经对视图定义进行了计算并且生成的数据像表一样存储。 可以为视图创建索引，即对视图创建一个唯一的聚集索引。 索引视图可以显著提高某些类型查询的性能。 索引视图尤其适于聚合许多行的查询。 但它们不太适于经常更新的基本数据集。  
  
 分区视图  
 分区视图在一台或多台服务器间水平连接一组成员表中的分区数据。 这样，数据看上去如同来自于一个表。 联接同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的成员表的视图是一个本地分区视图。  
  
 系统视图  
 系统视图公开目录元数据。 您可以使用系统视图返回与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例或在该实例中定义的对象有关的信息。 例如，你可以查询 sys.databases 目录视图以便返回与实例中提供的用户定义数据库有关的信息。 有关详细信息，请参阅[系统视图 (Transact-SQL)](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)。  
  
## <a name="common-view-tasks"></a>常见视图任务  
 下表提供指向与创建或修改视图相关联的常见任务的链接。  
  
|视图任务|主题|  
|----------------|-----------|  
|介绍如何创建视图。|[创建视图](../../relational-databases/views/create-views.md)|  
|介绍如何创建索引视图。|[创建索引视图](../../relational-databases/views/create-indexed-views.md)|  
|介绍如何修改视图定义。|[修改视图](../../relational-databases/views/modify-views.md)|  
|介绍如何通过视图修改数据。|[通过视图修改数据](../../relational-databases/views/modify-data-through-a-view.md)|  
|介绍如何删除视图。|[删除视图](../../relational-databases/views/delete-views.md)|  
|介绍如何返回与视图有关的信息，例如视图定义。|[获取有关视图的信息](../../relational-databases/views/get-information-about-a-view.md)|  
|介绍如何重命名视图。|[重命名视图](../../relational-databases/views/rename-views.md)|  
  
## <a name="see-also"></a>另请参阅  
 [基于 XML 列创建视图](../../relational-databases/xml/create-views-over-xml-columns.md)   
 [CREATE VIEW (Transact-SQL)](../../t-sql/statements/create-view-transact-sql.md)  
  
  
