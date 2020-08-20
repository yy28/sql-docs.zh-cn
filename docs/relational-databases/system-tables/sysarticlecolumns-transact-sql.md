---
description: sysarticlecolumns (Transact-SQL)
title: sysarticlecolumns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns system table
ms.assetid: 55918592-e05d-43b6-843b-7e4d82fa6275
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 45cc5fc3a39f13f7795e2f26aa91a15b618e2d38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460228"
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  对于快照发布或事务发布中发布的每个表列， **sysarticlecolumns** 表在表中各占一行，并将每个列映射到其项目。 该表存储在发布数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|标识项目。|  
|**colid**|**smallint**|标识项目中的列。|  
|**is_udt**|**bit**|表示列是否为用户定义数据类型 (UDT) 列。 值为 **1** 指示 UDT 列。|  
|**is_xml**|**bit**|指示列是否为 **xml** 列。 值 **1** 指示 xml 列。|  
|**is_max**|**bit**|指示列是否为大值数据类型列、 **varchar (max) **、 **nvarchar (max) **和 **varbinary (max) **。 值 **1** 表示大值列。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
