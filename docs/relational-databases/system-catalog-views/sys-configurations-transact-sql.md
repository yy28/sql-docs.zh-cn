---
title: sys.configurations (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fa2bae15b2da81dcf69ca1e486c74e7b4ccd5ba8
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044993"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  系统中每个服务器范围的配置选项值各占一行。  

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|配置值的唯一 ID。|  
|**名称**|**nvarchar(35)**|配置选项的名称。|  
|**value**|**sql_variant**|该选项的配置值。|  
|**最小值**|**sql_variant**|配置选项的最小值。|  
|**最大值**|**sql_variant**|配置选项的最大值。|  
|**value_in_use**|**sql_variant**|该选项当前使用的运行值。|  
|**description**|**nvarchar(255)**|配置选项的说明。|  
|**is_dynamic**|**bit**|1 = 执行 RECONFIGURE 语句时生效的变量。|  
|**is_advanced**|**bit**|1 = 该变量显示时，才**显示 advancedoption**设置。|  
  
 所有服务器配置选项的列表，请参阅[服务器配置选项&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
> [!NOTE]  
>  有关数据库级别配置选项，请参阅[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 若要配置软件 NUMA，请参阅[SOFT-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [服务器范围的配置目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
