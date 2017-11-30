---
title: "sp_helpdevice (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a39dcc6cd75837017826fdcf9b37ff7d6a3598c9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpdevice-transact-sql"></a>sp_helpdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告有关 Microsoft® SQL Server™ 备份设备的信息。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]我们建议你使用[sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)改用目录视图  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@devname =** ] *名称*  
 将为其报告信息的备份设备的名称。 值*名称*始终**sysname**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**设备名**|**sysname**|逻辑设备名。|  
|**physical_name**|**nvarchar(260)**|物理文件名。|  
|**description**|**nvarchar(255)**|设备的说明。|  
|**status**|**int**|到中的状态说明相对应的数字**说明**列。|  
|**cntrltype**|**int**|设备的控制器类型：<br /><br /> 2 = 磁盘设备<br /><br /> 5 = 磁带设备|  
|**大小**|**int**|设备大小（以 2 KB 页为单位）。|  
  
## <a name="remarks"></a>注释  
 如果*名称*指定，则**sp_helpdevice**显示有关指定的转储设备的信息。 如果*名称*未指定， **sp_helpdevice**显示信息中的所有转储设备**sys.backup_devices**目录视图。  
  
 转储设备通过使用添加到系统**sp_addumpdevice**。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例报告有关一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的所有转储设备的信息。  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_addumpdevice (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [数据库引擎存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
