---
title: sys.dm_os_loaded_modules (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_loaded_modules
- dm_os_loaded_modules
- sys.dm_os_loaded_modules_TSQL
- dm_os_loaded_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_loaded_modules dynamic management view
ms.assetid: 56c7743a-b568-4943-bd3b-73c57d9d641c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3967e3f8548a7b8ef804d054cf746243a8fb5b96
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63047185"
---
# <a name="sysdmosloadedmodules-transact-sql"></a>sys.dm_os_loaded_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  针对每个加载到服务器地址空间的模块返回一行。  
  
> [!NOTE]  
>  若要调用此项从[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_loaded_modules**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**base_address**|**varbinary(8)**|进程中的模块的地址。|  
|**file_version**|**varchar(23)**|文件的版本。 按如下格式显示：<br /><br /> x.x:x.x|  
|**product_version**|**varchar(23)**|产品版本。 按如下格式显示：<br /><br /> x.x:x.x|  
|**debug**|**bit**|1 = 模块是调试版本的已加载模块。|  
|**修补**|**bit**|1 = 模块已得到修补。|  
|**prerelease**|**bit**|1 = 模块是预发行版本的已加载模块。|  
|**private_build**|**bit**|1 = 模块是专用版本的已加载模块。|  
|**special_build**|**bit**|1 = 模块是特殊版本的已加载模块。|  
|**language**|**int**|模块的版本信息语言。|  
|**company**|**nvarchar(256)**|创建模块的公司的名称。|  
|**description**|**nvarchar(256)**|模块的说明。|  
|**名称**|**nvarchar(255)**|模块的名称。 包括模块的完整路径。|  
|**pdw_node_id**|**int**|适用于：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与 SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
