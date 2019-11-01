---
title: sys. database_scoped_configurations （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: da115c8d4cf48cfbcd6190c88a83bee4e61ae5a1
ms.sourcegitcommit: 27c267bf2a3cfaf2abcb5f3777534803bf4cffe5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240766"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>sys. database_scoped_configurations （Transact-sql）

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

每个配置占一行。 

|列名|“名称”|Description|
|-----------------|---------------|-----------------|
|**configuration_id**|**smallint**|配置选项的 ID。|
|**名称**|**nvarchar(60)**|配置选项的名称。 有关可能的配置的信息，请参阅[ALTER DATABASE 作用&#40;域配置 transact-sql&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|
|**value**|**sqlvariant**|为主副本的此配置选项设置的值。|
|**value_for_secondary**|**sqlvariant**|为辅助副本的此配置选项设置的值。|
|**is_value_default**|**bit** |指定设置的值是否为默认值。|

## <a name="Permissions"></a> Permissions

要求 **公共** 角色具有成员身份。

## <a name="remarks"></a>注释

如果返回 NULL 作为**value_for_secondary**的值，这意味着辅助数据库将设置为 PRIMARY。
 
数据库作用域内配置设置随数据库一同转入。 这意味着还原或附加给定数据库时，会保留现有配置设置。

## <a name="see-also"></a>另请参阅

[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
