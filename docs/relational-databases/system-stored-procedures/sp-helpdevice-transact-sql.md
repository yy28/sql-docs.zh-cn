---
title: sp_helpdevice （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cda03415378577a061bb308c0b19e7fcd0659d49
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893601"
---
# <a name="sp_helpdevice-transact-sql"></a>sp_helpdevice (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  报告有关 Microsoft® SQL Server™ 备份设备的信息。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]建议改用[sys.databases backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)目录视图  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @devname = ] 'name'`要报告其信息的备份设备的名称。 *Name*的值始终为**sysname**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**device_name**|**sysname**|逻辑设备名。|  
|**physical_name**|**nvarchar(260)**|物理文件名。|  
|**2008**|**nvarchar(255)**|设备的说明。|  
|**status**|**int**|与 "**说明**" 列中的状态说明相对应的数字。|  
|**cntrltype**|**smallint**|设备的控制器类型：<br /><br /> 2 = 磁盘设备<br /><br /> 5 = 磁带设备|  
|size |**int**|设备大小（以 2 KB 页为单位）。|  
  
## <a name="remarks"></a>备注  
 如果指定*name* ， **sp_helpdevice**将显示有关指定转储设备的信息。 如果未指定*name* ， **sp_helpdevice**将显示有关**sys.databases backup_devices**目录视图中的所有转储设备的信息。  
  
 使用**sp_addumpdevice**将转储设备添加到系统中。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例报告有关一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的所有转储设备的信息。  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_addumpdevice (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [数据库引擎存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
