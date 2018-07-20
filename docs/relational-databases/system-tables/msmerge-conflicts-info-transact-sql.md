---
title: MSmerge_conflicts_info (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_conflicts_info_TSQL
- MSmerge_conflicts_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflicts_info system table
ms.assetid: 6b76ae96-737a-4000-a6b6-fcc8772c2af4
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 41388cd1cc2d7a33f0b976ad62eca5e7f55aeade
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103635"
---
# <a name="msmergeconflictsinfo-transact-sql"></a>MSmerge_conflicts_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflicts_info**表跟踪订阅的合并发布同步时发生的冲突。 冲突的落选行数据存储在[MSmerge_conflict_publication_article](../../relational-databases/system-tables/msmerge-conflict-publication-article-transact-sql.md)项目发生冲突的表。 此表存储在发布服务器上的发布数据库中，并存储在订阅服务器上的订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|已发布表的别名。|  
|**rowguid**|**uniqueidentifier**|冲突行的标识符。|  
|**origin_datasource**|**nvarchar(255)**|发起冲突更改的数据库名。|  
|**conflict_type**|**int**|发生的冲突类型，可以为下列类型之一：<br /><br /> **1** = 更新冲突： 在行级别检测到冲突。<br /><br /> **2** = 列更新冲突： 在列级检测到冲突。<br /><br /> **3** = 更新删除入选冲突： 删除在冲突中获胜。<br /><br /> **4** = 更新入选删除冲突： 冲突中落选的已删除的 rowguid 将记录在此表。<br /><br /> **5** = 上载插入失败： 无法在发布服务器上应用来自订阅服务器上的插入。<br /><br /> **6** = 下载插入失败： 无法在订阅服务器上应用来自发布服务器的插入。<br /><br /> **7** = 上载删除失败： 无法上载到发布服务器在订阅服务器上删除。<br /><br /> **8** = 下载删除失败： 无法为发布服务器上的删除下载到订阅服务器。<br /><br /> **9** = 上载更新失败： 无法在发布服务器上应用在订阅服务器的更新。<br /><br /> **10** = 下载更新失败： 在发布服务器的更新无法应用于订阅服务器。<br /><br /> **11** = 解析<br /><br /> **12** = 逻辑记录更新入选删除： 在此表中记录冲突中落选的已删除逻辑记录。<br /><br /> **13** = 逻辑记录冲突插入更新： 指向逻辑记录的插入与更新冲突。<br /><br /> **14** = 逻辑记录删除入选更新冲突： 该表中记录的已更新的逻辑记录冲突中落选。|  
|**reason_code**|**int**|可能与上下文相关的错误代码。 在更新-更新和更新-删除冲突的情况下使用此列的值是与相同**conflict_type**。 但是，对于失败的更改冲突，原因代码是使合并代理无法应用更改的错误。 例如，如果由于主键冲突，合并代理无法应用插入，在订阅服务器，它记录**conflict_type** 6 （"下载插入失败"） 和一个**reason_code** 2627，这是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]主键冲突的内部错误消息:"违反了 %ls 约束 ' %.* ls'。 不能在对象中插入重复键 %。\*ls'。"|  
|**reason_text**|**nvarchar(720)**|可能与上下文相关的错误说明。|  
|**pubid**|**uniqueidentifier**|发布的标识符。|  
|**MSrepl_create_time**|**datetime**|冲突发生的时间。|  
|**origin_datasource_id**|**uniqueidentifier**|发起冲突更改的数据库的标识符。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
