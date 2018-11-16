---
title: sys.dm_os_windows_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_windows_info
- dm_os_windows_info_TSQL
- sys.dm_os_windows_info
- sys.dm_os_windows_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_windows_info dynamic management view
ms.assetid: adc81283-fdc2-46c0-bb48-abe82bbf2459
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f258d7e49f86ed8015d8e51f2373633b7d7f10c4
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51663133"
---
# <a name="sysdmoswindowsinfo-transact-sql"></a>sys.dm_os_windows_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个显示 Windows 操作系统版本信息的行。  
  
  仅适用于在 Windows 上运行的 SQL Server。 若要运行非 Windows 主机，如 Linux 上的 SQL Server，请参阅类似信息时使用[sys.dm_os_host_info &#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)。 
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar(256)**|对于 Windows，返回发行版号。 有关值和说明的列表，请参阅[操作系统版本 (Windows)](/windows/desktop/SysInfo/operating-system-version)。 不能为 NULL。|  
|**windows_service_pack_level**|**nvarchar(256)**| 对于 Windows，返回的 service pack 编号。 不能为 NULL。 |  
|**windows_sku**|**int**|对于 Windows，将返回 Windows 库存单位 (SKU) id。 有关 SKU Id 和说明的列表，请参阅[GetProductInfo 函数](https://msdn.microsoft.com/library/ms724358.aspx)。 可以为 Null。 |  
|**os_language_version**|**int**| 对于 Windows，返回的操作系统的 Windows 区域设置标识符 (LCID)。 有关 LCID 值和说明的列表，请参阅[由 Microsoft 分配的区域设置 Id](https://go.microsoft.com/fwlink/?LinkId=208080)。 不能为 NULL。|  
  
  
## <a name="permissions"></a>Permissions  
默认情况下，sys.dm_os_windows_info 拥有 SELECT 权限授予公共角色。 如果吊销，需要在服务器上的 VIEW SERVER STATE 权限。  

## <a name="limitations-and-restrictions"></a>限制和局限
若要运行非 Windows 主机，如 Linux 上的 SQL，请参阅信息时使用[sys.dm_os_host_info &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)。 
  
## <a name="examples"></a>示例  
 下面的示例返回中的所有列**sys.dm_os_windows_info**视图。  
  
```  
SELECT windows_release, windows_service_pack_level, windows_sku, os_language_version  
FROM sys.dm_os_windows_info;  
```  
  
 下面是一个结果集示例。  
  
 `windows_release  windows_service_pack_level   windows_sku   os_language_version`  
  
 `---------------  ---------------------------  ------------  -------------------`  
  
 `6.0              Service Pack 2                4            1033`  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)  
  
  

