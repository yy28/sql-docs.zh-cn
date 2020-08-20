---
description: 'sys. dm_os_enumerate_fixed_drives (Transact-sql) '
title: sys. dm_os_enumerate_fixed_drives (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/18/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_enumerate_fixed_drives
- sys.dm_os_enumerate_fixed_drives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_enumerate_fixed_drives dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6be0f2083a39bad3d232fd3105fa94c92fb71640
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454921"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>sys. dm_os_enumerate_fixed_drives (Transact-sql) 

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

在 SQL Server 2019 中引入。

枚举装载到驱动器号的卷，例如 `C:\` 。

|列名称|数据类型|说明|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|卷的路径，如 `C:\` 。|  
|`drive_type`|`int`|驱动器类型的代码。 请参阅[ `GetDriveTypeW` 函数](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)。|
|`drive_type_desc`|`nvarchar(512)`|驱动器类型的说明。 请参阅[ `GetDriveTypeW` 函数](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)。|
|`free_space_in_bytes`|`bigint`|磁盘可用空间（以字节为单位）。|

## <a name="permissions"></a>权限

用户必须具有 `VIEW SERVER STATE` 对服务器的权限。

## <a name="see-also"></a>另请参阅  

 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与 i/o 相关的动态管理视图和函数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
