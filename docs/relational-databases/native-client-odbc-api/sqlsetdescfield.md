---
title: SQLSetDescField |微软文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f699610ce3aac1443439aa5d293e92104f3033d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292037"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSetDescField 可用于为表值参数和表值参数列设置描述符字段。 有关可用字段的信息，请参阅[表值参数构成列](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)的[表-值参数描述字段](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)和描述字段。  
  
## <a name="remarks"></a>备注  
 表值参数列仅在将描述符标头字段 SQL_SOPT_SS_PARAM_FOCUS 设置为特定记录（其 SQL_DESC_TYPE 设置为 SQL_SS_TABLE）的序数时可用。 有关SQL_SOPT_SS_PARAM_FOCUS的详细信息，请参阅[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 如果尝试将SQL_SOPT_SS_PARAM_FOCUS设置为非表值参数的参数的表位，SQLSetStmtAttr 将返回SQL_ERROR，并且使用 SQLSTATE = HY024 和消息"无效属性值"创建诊断记录。 返回 SQL_ERROR 时，不更改 SQL_SOPT_SS_PARAM_FOCUS。  
  
 将 SQL_SOPT_SS_PARAM_FOCUS 设置为 0 可以恢复对参数的描述符记录的访问权限。  
  
 有关表值参数的详细信息，请参阅[&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>SQLSetDescField 对日期和时间增强功能的支持  
 ODBC 中已增强了日期/时间功能。 有关为新日期/时间类型提供的描述符字段的信息，请参阅[参数和结果元数据](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 有关详细信息，请参阅[&#40;ODBC&#41;的日期和时间改进](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>SQLSetDescField 对大型 CLR UDT 的支持  
 SQLSetDescField 支持大型 CLR 用户定义类型 （UDT）。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>SQLSetDescField 对稀疏列的支持  
 SQLSetDecField 可用于在应用程序参数描述符 （APD） 中设置SQL_SOPT_SS_NAME_SCOPESQL_SS_NAME_SCOPE_EXTENDED和SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET值。  
  
 有关详细信息，请参阅[稀疏列支持&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
