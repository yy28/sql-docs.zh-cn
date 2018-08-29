---
title: 日期和时间改进 (OLE DB) |Microsoft Docs
description: 日期和时间改进 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 5bcfb89323051470dc307a8b4828ee6d8dc000a5
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025776"
---
# <a name="date-and-time-improvements-ole-db"></a>日期和时间改进 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 引入了新的日期和时间数据类型。 本部分介绍这些新类型适用于 SQL Server 的公开为扩展的 OLE DB 驱动程序。 SQL Server 支持的新的日期和时间数据类型，OLE DB 驱动程序的概述，请参阅[日期和时间改进](../../oledb/features/date-and-time-improvements.md)。 有关示例，请参阅[使用增强的日期和时间功能&#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)。  
  
 有关日期和时间数据类型的更多常规信息，请参阅[datetime &#40;TRANSACT-SQL&#41;](../../../t-sql/data-types/datetime-transact-sql.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [针对 OLE DB 日期和时间改进的数据类型支持](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 提供了有关 OLE DB （OLE DB 驱动程序适用于 SQL Server） 的信息类型的支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]日期和时间数据类型。  
  
 [元数据&#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 包含有关 DBBINDING 结构的信息**icommandwithparameters:: Getparameterinfo**， **icommandwithparameters:: Setparameterinfo**， **IColumnsRowset::GetColumnsRowset**，和我**ColumnsInfo::GetColumnInfo**。 还提供了有关 OLE DB 架构行集更新的信息。  
  
 [绑定和转换 (OLE DB)](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 说明在服务器和客户端之间现有和新数据类型的转换规则。  
  
 [增强的日期和时间类型的大容量复制更改 (OLE DB)](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 描述支持大容量复制操作的日期/时间增强功能。  
  
 [OLE DB API 对日期和时间增强功能的支持](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 说明支持日期/时间增强功能的 OLE DB API。  
  
 [IRowsetFind 的可比性](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 介绍了日期/时间类型和**IRowsetFind**。  
 
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
