---
title: "表值参数数据转换和其他错误和警告 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 328b555b30fb28e623012d5e52cc7296712be22a
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>表值参数数据转换及其他错误和警告
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  表值参数列值可按照与其他列和参数值相同的方式在客户端和服务器数据类型之间转换。 但是由于表值参数可以包含多个列和多个行，所以必须能够标识出现错误的实际值，这一点很重要。  
  
 当在表值参数列中检测到错误或警告时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将生成诊断记录。 错误消息将包含表值参数的参数编号，以及列序号和行号。 应用程序还可以使用诊断记录中的诊断字段 SQL_DIAG_SS_TABLE_COLUMN_NUMBER 和 SQL_DIAG_SS_TABLE_ROW_NUMBER 确定与错误和警告关联的值。 这些诊断字段在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中提供。  
  
 诊断记录的 SQLSTATE 和消息部分将在所有其他方面符合现有的 ODBC 行为。 也就是说，除参数、行和列标识信息之外，表值参数与非表值参数具有相同的错误消息值。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
