---
title: sys.databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 885b736424dfa0b1a83f0d0c854fc11b80f67ade
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832762"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  系统中每个服务器范围的配置选项值各占一行。  

|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|配置值的唯一 ID。|  
|**name**|**nvarchar(35)**|配置选项的名称。|  
|**value**|**sql_variant**|该选项的配置值。|  
|**短**|**sql_variant**|配置选项的最小值。|  
|**最佳**|**sql_variant**|配置选项的最大值。|  
|**value_in_use**|**sql_variant**|该选项当前使用的运行值。|  
|**2008**|**nvarchar(255)**|配置选项的说明。|  
|**is_dynamic**|**bit**|1 = 执行 RECONFIGURE 语句时生效的变量。|  
|**is_advanced**|**bit**|1 = 只有在设置了**show advancedoption**时才会显示变量。|  
  
 有关所有服务器配置选项的列表，请参阅[服务器配置选项 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
> [!NOTE]  
>  有关数据库级配置选项，请参阅[ALTER DATABASE 作用域配置 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 若要配置软件 NUMA，请参阅[软 numa &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [服务器范围内的配置目录视图 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
