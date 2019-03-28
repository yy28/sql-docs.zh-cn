---
title: sp_helpdevice (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c856e11b55040bf699eace2fb1f917f058c2fc9a
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536369"
---
# <a name="sphelpdevice-transact-sql"></a>sp_helpdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告有关 Microsoft® SQL Server™ 备份设备的信息。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我们建议你使用[sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)目录视图  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @devname = ] 'name'` 是要报告其信息的备份设备的名称。 值*名称*始终**sysname**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**device_name**|**sysname**|逻辑设备名。|  
|**physical_name**|nvarchar(260)|物理文件名。|  
|**description**|**nvarchar(255)**|设备的说明。|  
|**status**|**int**|对应于状态说明中的数字**说明**列。|  
|**cntrltype**|**smallint**|设备的控制器类型：<br /><br /> 2 = 磁盘设备<br /><br /> 5 = 磁带设备|  
|size|**int**|设备大小（以 2 KB 页为单位）。|  
  
## <a name="remarks"></a>备注  
 如果*名称*指定，则**sp_helpdevice**显示有关指定的转储设备的信息。 如果*名称*未指定，则**sp_helpdevice**显示有关中的所有转储设备的信息**sys.backup_devices**目录视图。  
  
 转储设备通过使用添加到系统**sp_addumpdevice**。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例报告有关一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的所有转储设备的信息。  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_addumpdevice (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
