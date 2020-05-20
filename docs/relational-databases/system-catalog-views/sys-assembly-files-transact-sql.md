---
title: sys. assembly_files （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.assembly_files
- assembly_files_TSQL
- assembly_files
- sys.assembly_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_files catalog view
ms.assetid: 1a384a2c-5556-4d12-a2ba-4da781363143
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4a30ad97dde1c27518976fc6ee631104b5fef7d4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831887"
---
# <a name="sysassembly_files-transact-sql"></a>sys.assembly_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  组成程序集的每个文件在表中各对应一行。  
    
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|此文件所属的程序集的 ID。|  
|**name**|**nvarchar(260)**|程序集文件的名称。|  
|**file_id**|**int**|文件的 ID。 在程序集中是唯一的。 编号为 1 的文件 ID 表示程序集 DLL。|  
|**content**|**varbinary(max)**|文件的内容。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的 CLR 程序集目录视图](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
