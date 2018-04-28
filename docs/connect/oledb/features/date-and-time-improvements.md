---
title: 日期和时间改进 |Microsoft 文档
description: 日期和时间中的改进 OLE DB 驱动程序的 SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d6b287b7cf96ec91ce776dd65bcec01e8c777a1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="date-and-time-improvements"></a>日期和时间的改进
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主题介绍用于在中添加了日期和时间数据类型的 SQL Server 支持的 OLE DB 驱动程序[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  
  
 有关日期/时间的改进的详细信息，请参阅[日期和时间改进&#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)。  
  
 有关演示此功能的示例应用程序的信息，请参阅[SQL Server 数据编程示例](http://msftdpprodsamples.codeplex.com/)。  
  
## <a name="usage"></a>用法  
 以下各节介绍使用新的日期和时间类型的各种方法。  
  
### <a name="use-date-as-a-distinct-data-type"></a>将日期用作非重复数据类型  
 开头[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]，增强了对日期/时间类型支持使使用 DBTYPE_DBDATE OLE DB 类型更加高效。  
  
### <a name="use-time-as-a-distinct-data-type"></a>将时间用作非重复数据类型  
 OLE DB 已具有一种只包含时间的数据类型 DBTYPE_DBTIME，它的精度为 1 秒。
  
 新[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]时间数据类型具有小数秒精确到 100 纳秒。 这需要 SQL Server 的 OLE DB 驱动程序中的新类型： DBTYPE_DBTIME2。 已编写的所用时间不带秒的小数部分的现有应用程序可以使用 time(0) 列。 现有的 OLE DB DBTYPE_TIME 类型和其相应的结构应正常工作，除非应用程序依赖于在元数据中返回的类型。  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>将具有扩展的秒的小数部分精度的时间用作非重复数据类型  
 某些应用程序（如过程控制和生产应用程序）要求能够处理精度高达 100 纳秒的时间数据。 为此目的在 OLE DB 的新类型是 DBTYPE_DBTIME2。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>使用具有扩展的秒的小数部分精度的日期时间  
 OLE DB 已定义了一个精度高达 1 纳秒的类型。 但是，此类型已由现有的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 应用程序使用，并且此类应用程序预计只需 1/300 秒精度。 新**datetime2(3)** 类型不是直接与现有的 datetime 类型兼容。 如果这一点将影响应用程序行为而导致风险，则应用程序必须使用新的 DBCOLUMN 标志以确定实际的服务器类型。    
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>使用具有扩展的秒的小数部分精度和时区的日期时间  
 一些应用程序要求带有时区信息的日期时间值。 通过新的 DBTYPE_DBTIMESTAMPOFFSET 类型支持此功能。
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>将 Date/Time/Datetime/Datetimeoffset 数据用于与现有转换一致的客户端转换  
 转换进行了扩展以一致的方式为包括所有中引入的日期和时间类型之间的转换[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
