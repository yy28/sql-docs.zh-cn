---
title: 运行存储的过程 (OLE DB) |Microsoft 文档
description: 运行存储过程 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf576884f19f10ae7e82bc479229155775d674f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="stored-procedures---running"></a>存储的过程的运行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在执行语句时，可以提供在数据源 （而不是执行或直接准备客户端应用程序中的语句） 上调用存储的过程：  
  
-   提高性能。  
  
-   降低网络开销。  
  
-   提供更好的一致性。  
  
-   提高准确性。  
  
-   增加功能。  
  
 SQL Server 的 OLE DB 驱动程序支持三种机制，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]存储的过程用于返回数据：  
  
-   在过程中的每个 SELECT 语句生成的结果集。  
  
-   过程可以通过输出参数返回数据。  
  
-   过程可以具有整数返回代码。  
  
 应用程序必须能够处理所有这些输出的存储过程。  
  
 在结果处理期间，不同的 OLE DB 访问接口返回输出参数和返回值的时间不同。 OLE DB 驱动程序的 SQL Server，如果输出参数和返回代码未提供直到后使用者已检索到或取消的存储过程返回的结果集。 返回代码和输出参数在最后一个来自服务器的 TDS 数据包中返回。  
  
 访问接口返回输出参数和返回值时，使用 DBPROP_OUTPUTPARAMETERAVAILABILITY 属性进行报告。 此属性位于 DBPROPSET_DATASOURCEINFO 属性集中。  
  
 SQL Server 的 OLE DB 驱动程序将 DBPROP_OUTPUTPARAMETERAVAILABILITY 属性设置为 DBPROPVAL_OA_ATROWRELEASE 以指示，在处理结果集或将其发布之前不返回返回代码和输出参数。  
  
## <a name="see-also"></a>另请参阅  
 [存储的过程](../../oledb/ole-db/stored-procedures.md)  
  
  
