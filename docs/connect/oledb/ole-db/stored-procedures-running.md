---
title: 运行存储的过程 (OLE DB) |Microsoft Docs
description: 运行存储过程 (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: a016e7c0d6ffb59b01ab679bbe21029558f7966b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830785"
---
# <a name="stored-procedures---running"></a>存储过程 - 运行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  执行语句时，对数据源调用存储过程（而不是直接在客户端应用程序中执行或准备语句）可以：  
  
-   提高性能。  
  
-   降低网络开销。  
  
-   提供更好的一致性。  
  
-   提高准确性。  
  
-   增加功能。  
  
 适用于 SQL Server 的 OLE DB 驱动程序支持三种机制，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]存储的过程用于返回数据：  
  
-   过程中的每一条 SELECT 语句都生成一个结果集。  
  
-   过程可以通过输出参数返回数据。  
  
-   过程可以具有整数返回代码。  
  
 应用程序必须能够处理来自存储过程的所有这些输出。  
  
 在结果处理期间，不同的 OLE DB 访问接口返回输出参数和返回值的时间不同。 对于适用于 SQL Server 的 OLE DB 驱动程序，直到使用者检索或取消了存储过程所返回的结果集之后，才提供输出参数和返回代码。 返回代码和输出参数在最后一个来自服务器的 TDS 数据包中返回。  
  
 访问接口返回输出参数和返回值时，使用 DBPROP_OUTPUTPARAMETERAVAILABILITY 属性进行报告。 此属性位于 DBPROPSET_DATASOURCEINFO 属性集中。  
  
 适用于 SQL Server 的 OLE DB 驱动程序将 DBPROP_OUTPUTPARAMETERAVAILABILITY 属性设置为 DBPROPVAL_OA_ATROWRELEASE，以指示直到处理或释放结果集之后才返回返回代码和输出参数。  
  
## <a name="see-also"></a>另请参阅  
 [存储过程](../../oledb/ole-db/stored-procedures.md)  
  
  
