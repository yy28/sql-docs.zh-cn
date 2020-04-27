---
title: sys. dm_os_windows_info （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: d25713ba8fb298ce465910eae786befb710961d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899584"
---
# <a name="sysdm_os_windows_info-transact-sql"></a>sys.dm_os_windows_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个显示 Windows 操作系统版本信息的行。  
  
  仅适用于在 Windows 上运行的 SQL Server。 若要查看在非 Windows 主机（如 Linux）上运行 SQL Server 的类似信息，请使用[sys. dm_os_host_info &#40;transact-sql&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)。 
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar(256)**|对于 Windows，返回发布号。 有关值和说明的列表，请参阅[操作系统版本（Windows）](/windows/desktop/SysInfo/operating-system-version)。 不能为 NULL。|  
|**windows_service_pack_level**|**nvarchar(256)**| 对于 Windows，将返回 Service Pack 号。 不能为 NULL。 |  
|**windows_sku**|**int**|对于 Windows，返回 Windows 库存单位（SKU） ID。 有关 SKU Id 和说明的列表，请参阅[GetProductInfo 函数](https://msdn.microsoft.com/library/ms724358.aspx)。 可以为 Null。 |  
|**os_language_version**|**int**| 对于 Windows，返回操作系统的 Windows 区域设置标识符（LCID）。 有关 LCID 值和说明的列表，请参阅[Microsoft 分配的区域设置 id](https://go.microsoft.com/fwlink/?LinkId=208080)。 不能为 NULL。|  
  
  
## <a name="permissions"></a>权限  
默认情况下，将对 dm_os_windows_info sys.databases 的 SELECT 权限授予 public 角色。 如果已吊销，则需要对服务器具有 VIEW SERVER STATE 权限。  

## <a name="limitations-and-restrictions"></a>限制和局限
若要查看在非 Windows 主机（如 Linux）上运行的 SQL 的信息，请使用[&#40;transact-sql&#41;上的 sys. dm_os_host_info ](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)。 
  
## <a name="examples"></a>示例  
 下面的示例返回**sys.databases dm_os_windows_info**视图中的所有列。  
  
```  
SELECT windows_release, windows_service_pack_level, windows_sku, os_language_version  
FROM sys.dm_os_windows_info;  
```  
  
 下面是一个结果集示例。  
  
 `windows_release  windows_service_pack_level   windows_sku   os_language_version`  
  
 `---------------  ---------------------------  ------------  -------------------`  
  
 `6.0              Service Pack 2                4            1033`  
  
## <a name="see-also"></a>另请参阅  
 [sys. dm_os_sys_info &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)  
  
  

