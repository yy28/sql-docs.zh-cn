---
title: sys.database_scoped_configurations (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3439419bd3877b8ab7a951df58585703f169ee4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079453"
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含每个配置的一行。 
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|配置选项的 ID。|  
|**name**|**nvarchar(60)**|配置选项的名称。 有关可能的配置信息，请参阅[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|  
|**value**|**sqlvariant**|对于主副本此配置选项设置的值。|  
|**value_for_secondary**|**sqlvariant**|设置次要副本的此配置选项的值。|  
|**is_value_default**|**bit** |指定设置的值是否为默认值。|
  
##  <a name="Permissions"></a> Permissions  
要求 **公共** 角色具有成员身份。  
  
## <a name="remarks"></a>备注  
值返回 NULL **value_for_secondary**，这意味着，辅助数据库设置为主要。  
 
数据库作用域内配置设置随数据库一同转入。 这意味着还原或附加给定数据库时，会保留现有配置设置。
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
