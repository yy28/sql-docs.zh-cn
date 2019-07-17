---
title: sys.time_zone_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.time_zone_info
- sys.time_zone_info_TSQL
- time_zone_info
- time_zone_info_TSQL
helpviewer_keywords:
- sys.time_zone_info system table
ms.assetid: 3f51a9a4-75f8-4a11-9552-8bf6118b68da
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 69bfcbb7e1eeaf6b456a2e10d1f3bfcc581c3d76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106706"
---
# <a name="systimezoneinfo-transact-sql"></a>sys.time_zone_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  返回有关受支持的时区信息。 在计算机上安装的所有时间区域都存储在以下注册表配置单元：  
`KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Windows 标准格式中的时区的名称。 例如， **cen。澳大利亚标准时间**或**中欧标准时间**。|  
|**current_utc_offset**|**nvarchar(12)**|当前为 UTC 的偏移量。 例如， **+ 01:00**或 **-07:00**。|  
|**is_currently_dst**|**bit**|如果当前观察夏时制，则为 true。|  
  
## <a name="see-also"></a>请参阅  
 [GETUTCDATE &#40;Transact-SQL&#41;](../../t-sql/functions/getutcdate-transact-sql.md)   
 [AT TIME ZONE (Transact-SQL)](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [日期和时间数据类型及函数 (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [服务器范围的配置目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)  
