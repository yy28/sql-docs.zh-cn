---
title: sp_helpmergeconflictrows (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpmergeconflictrows_TSQL
- sp_helpmergeconflictrows
helpviewer_keywords:
- sp_helpmergeconflictrows
ms.assetid: 131395a5-cb18-4795-a7ae-fa09d8ff347f
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3972f0bee0e172d19ddc205fc9d8aa6a314d89cf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpmergeconflictrows-transact-sql"></a>sp_helpmergeconflictrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定冲突表中的行。 此存储过程在存储冲突表的计算机上运行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpmergeconflictrows [ [ @publication = ] 'publication' ]  
        , [ @conflict_table = ] 'conflict_table'  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publsher_db' ]   
    [ , [ @logical_record_conflicts = ] logical_record_conflicts ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，默认值为**%**。 如果指定了发布，将返回由该发布限定的所有冲突。 例如，如果**MSmerge_conflict_Customers**表具有冲突行**WA**和**CA**发布，发布名称传入**CA**检索冲突属于**CA**发布。  
  
 [  **@conflict_table=**] *****conflict_table*****  
 冲突表的名称。 *conflict_table*是**sysname**，无默认值。 在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和更高版本，命名冲突表使用的格式名与 **MSmerge_conflict_*发布*_*文章 * * *，与为每个发布的一个表文章。  
  
 [ **@publisher=**] **'***publisher***'**  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 是发布服务器数据库的名称。*publisher_db*是**sysname**，默认值为 NULL。  
  
 [  **@logical_record_conflicts=** ] *logical_record_conflicts*  
 指示结果集是否包含有关逻辑记录冲突的信息。 *logical_record_conflicts*是**int**，默认值为 0。 **1**意味着返回逻辑记录冲突信息。  
  
## <a name="result-sets"></a>结果集  
 **sp_helpmergeconflictrows**返回的结果集的基表结构和这些额外的列组成。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar(255)**|冲突的起源。|  
|**conflict_type**|**int**|表示冲突类型的代码：<br /><br /> **1** = 更新冲突： 在行级检测到冲突。<br /><br /> **2** = 列更新冲突： 列级检测到冲突。<br /><br /> **3** = 更新删除 Wins 冲突： 删除在冲突中获胜。<br /><br /> **4** = 更新 Wins 删除冲突： 在此表中记录失去冲突已删除的 rowguid。<br /><br /> **5** = 上载插入失败： 无法在发布服务器上应用从订阅服务器插入。<br /><br /> **6** = 下载插入失败： 无法在订阅服务器上应用从发布服务器插入。<br /><br /> **7** = 上载删除失败： 无法将订阅服务器上的删除上载到发布服务器。<br /><br /> **8** = 下载删除失败： 无法下载到订阅服务器在发布服务器上删除。<br /><br /> **9** = 上载更新失败： 无法在发布服务器上应用在订阅服务器上更新。<br /><br /> **10** = 下载更新失败： 在发布服务器上更新无法应用于订阅服务器。<br /><br /> **12** = 逻辑记录更新 Wins Delete： 在此表中记录失去冲突的已删除逻辑记录。<br /><br /> **13** = 逻辑记录冲突插入更新： 与更新到逻辑记录的插入冲突。<br /><br /> **14** = 逻辑记录删除 Wins 更新冲突： 在此表中记录了失去冲突的更新的逻辑记录。|  
|**reason_code**|**int**|与上下文相关的错误代码。|  
|**reason_text**|**varchar(720)**|与上下文相关的错误说明。|  
|**pubid**|**uniqueidentifier**|发布标识符。|  
|**MSrepl_create_time**|**datetime**|添加冲突信息的时间。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpmergeconflictrows**合并复制中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定服务器角色、 **db_owner**固定数据库角色和**replmonitor**分发数据库中的角色可以执行**sp_helpmergeconflictrows**。  
  
## <a name="see-also"></a>另请参阅  
 [查看合并发布的冲突信息&#40;复制 TRANSACT-SQL 编程&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
