---
title: sys.dm_os_host_info (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 613b7884342750e84aa6f6476bc040c2dd37bead
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmoshostinfo-transact-sql"></a>sys.dm_os_host_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

返回一行显示操作系统版本信息。  
  
|列名 |数据类型 |Description |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |一种操作系统： Windows 或 Linux |
|**host_distribution** |**nvarchar(256)** |操作系统的说明。 |
|**host_release**|**nvarchar(256)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 操作系统版本（版本号） 有关值和说明的列表，请参阅[操作系统版本 (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx)。 <br> 对于 Linux，返回一个空字符串。 |  
|**host_service_pack_level**|**nvarchar(256)**|Windows 操作系统的 Service Pack 级别。 <br> 对于 Linux，返回一个空字符串。 |  
|**host_sku**|**int**|Windows 单品 (SKU) ID。 SKU Id 和说明的列表，请参阅[GetProductInfo 函数](http://msdn.microsoft.com/library/ms724358.aspx)。 可以为 Null。 <br> 适用于 Linux，则返回 NULL。 |  
|**os_language_version**|**int**|操作系统的 Windows 区域设置标识符 (LCID)。 LCID 值和说明的列表，请参阅[由 Microsoft 分配的区域设置 Id](http://go.microsoft.com/fwlink/?LinkId=208080)。 不可为 null。|  

## <a name="remarks"></a>注释  
此视图是类似于[sys.dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)，添加列来区分 Windows 和 Linux。
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
`SELECT`权限`sys.dm_os_host_info`权限已授予`public`默认情况下的角色。 如果被吊销，则需要`VIEW SERVER STATE`服务器上的权限。   
 
>  [!CAUTION]
>  从版本开始[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.3[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)]版本 17 需要`SELECT`权限`sys.dm_os_host_info`以便连接到[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 如果`SELECT`从撤消权限`public`，仅有的登录名`VIEW SERVER STATE`权限可以使用最新版本的 SSMS 连接。 (其他工具，如`sqlcmd.exe`可以连接而无需`SELECT`权限`sys.dm_os_host_info`。)

  
## <a name="examples"></a>示例  
 下面的示例返回中的所有列**sys.dm_os_host_info**视图。  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

下面是在 Windows 上设置的示例结果：
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |2052 |  

下面是在 Linux 上设置的示例结果：
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |2052 |  

  
## <a name="see-also"></a>另请参阅  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

