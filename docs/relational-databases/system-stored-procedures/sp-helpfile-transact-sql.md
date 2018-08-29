---
title: sp_helpfile (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpfile
- sp_helpfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 74acb22b50ce918f070c817cb8954b46e47bb876
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023835"
---
# <a name="sphelpfile-transact-sql"></a>sp_helpfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回与当前数据库关联的文件的物理名称及属性。 使用此存储过程确定附加到服务器或从服务器分离的文件名。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@filename =** ] **'***name***'**  
 当前数据库中任意文件的逻辑名称。 *名称*是**sysname**，默认值为 NULL。 如果*名称*是未指定，将返回当前数据库中的所有文件的属性。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|逻辑文件名称。|  
|**fileid**|**smallint**|文件的数字标识符。 如果不返回*名称*指定 *。*|  
|**filename**|**nchar(260)**|物理文件名。|  
|**filegroup**|**sysname**|文件所属的文件组。<br /><br /> NULL = 文件是日志文件。 它决不是文件组的一部分。|  
|size|**nvarchar(15)**|文件大小 (KB)。|  
|**最大大小**|**nvarchar(15)**|文件大小可达到的最大值。 此字段中的 UNLIMITED 值表示文件可以一直增长到磁盘变满为止。|  
|**增长**|**nvarchar(15)**|文件的增量。 表示每次需要新空间时为文件增加的空间大小。<br /><br /> 0 = 文件的大小是固定的，不会增长。|  
|**使用情况**|**varchar(9)**|对于数据文件的值是**仅限数据**并为日志文件的值是**仅记录**。|  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例返回有关 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中的文件的信息。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfile;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfilegroup (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据库文件和文件组](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
