---
title: MSmerge_conflicts_info (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c2376ff24d94a8360bd39686fb71f0b4d94a2b4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="msmergeconflictsinfo-transact-sql"></a>MSmerge_conflicts_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflicts_info**表跟踪出现同步对合并发布的订阅时的冲突。 为冲突落选行数据存储在[MSmerge_conflict_publication_article](../../relational-databases/system-tables/msmerge-conflict-publication-article-transact-sql.md)项目发生了冲突的表。 此表存储在发布服务器上的发布数据库中，并存储在订阅服务器上的订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|已发布表的别名。|  
|**rowguid**|**uniqueidentifier**|冲突行的标识符。|  
|**origin_datasource**|**nvarchar(255)**|发起冲突更改的数据库名。|  
|**conflict_type**|**int**|发生的冲突类型，可以为下列类型之一：<br /><br /> **1** = 更新冲突： 在行级检测到冲突。<br /><br /> **2** = 列更新冲突： 列级检测到冲突。<br /><br /> **3** = 更新删除 Wins 冲突： 删除在冲突中获胜。<br /><br /> **4** = 更新 Wins 删除冲突： 在此表中记录失去冲突已删除的 rowguid。<br /><br /> **5** = 上载插入失败： 无法在发布服务器上应用从订阅服务器插入。<br /><br /> **6** = 下载插入失败： 无法在订阅服务器上应用从发布服务器插入。<br /><br /> **7** = 上载删除失败： 无法将订阅服务器上的删除上载到发布服务器。<br /><br /> **8** = 下载删除失败： 无法下载到订阅服务器在发布服务器上删除。<br /><br /> **9** = 上载更新失败： 无法在发布服务器上应用在订阅服务器上更新。<br /><br /> **10** = 下载更新失败： 在发布服务器上更新无法应用于订阅服务器。<br /><br /> **11** = 解析<br /><br /> **12** = 逻辑记录更新 Wins Delete： 在此表中记录失去冲突的已删除逻辑记录。<br /><br /> **13** = 逻辑记录冲突插入更新： 与更新到逻辑记录的插入冲突。<br /><br /> **14** = 逻辑记录删除 Wins 更新冲突： 在此表中记录了失去冲突的更新的逻辑记录。|  
|**reason_code**|**int**|可能与上下文相关的错误代码。 在更新-更新，并在更新-删除冲突的情况下使用此列的值是相同**conflict_type**。 但是，对于失败的更改冲突，原因代码是使合并代理无法应用更改的错误。 例如，如果合并代理无法将订阅服务器上的插入应用由于主键冲突，它记录**conflict_type**的 6 （"下载插入失败"） 和一个**reason_code**的 2627，即[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]主键冲突的内部错误消息:"%ls 约束冲突 %.* ls。 无法在对象中插入重复键 %。\*ls。"|  
|**reason_text**|**nvarchar(720)**|可能与上下文相关的错误说明。|  
|**pubid**|**uniqueidentifier**|发布的标识符。|  
|**MSrepl_create_time**|**datetime**|冲突发生的时间。|  
|**origin_datasource_id**|**uniqueidentifier**|发起冲突更改的数据库的标识符。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
