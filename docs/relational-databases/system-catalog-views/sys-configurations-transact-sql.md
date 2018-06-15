---
title: sys.configurations (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 25de8a6eb70c79551caca8188c4f67a786e62172
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181713"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  系统中每个服务器范围的配置选项值各占一行。  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|配置值的唯一 ID。|  
|**名称**|**nvarchar(35)**|配置选项的名称。|  
|**值**|**sql_variant**|该选项的配置值。|  
|**最小值**|**sql_variant**|配置选项的最小值。|  
|**最大值**|**sql_variant**|配置选项的最大值。|  
|**value_in_use**|**sql_variant**|该选项当前使用的运行值。|  
|**说明**|**nvarchar(255)**|配置选项的说明。|  
|**is_dynamic**|**bit**|1 = 执行 RECONFIGURE 语句时生效的变量。|  
|**is_advanced**|**bit**|1 = 显示该变量时，才**显示 advancedoption**设置。|  
  
 所有服务器配置选项的列表，请参阅[服务器配置选项&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
> [!NOTE]  
>  有关数据库级配置选项，请参阅[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 若要配置 SOFT-NUMA，请参阅[SOFT-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [服务器范围的配置目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
