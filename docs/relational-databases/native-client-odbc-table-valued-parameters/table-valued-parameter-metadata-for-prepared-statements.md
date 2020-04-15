---
title: 已准备语句的 TVP 元数据
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6928c24b1c06e75c8e20b318321eac4f4bd99985
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297746"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>准备的语句的表值参数元数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  应用程序可以通过 SQLNumParams 和 SQLDescribeParam 获取已准备好的过程调用的元数据。 对于表值参数 *，DataTypePtr*设置为SQL_SS_TABLE。 其他元数据可通过 SQLGetDescField 用于SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME和SQL_CA_SS_SCHEMA_NAME。  
  
 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME和SQL_CA_SS_SCHEMA_NAME可与 SQLColumn 一起使用，以获取与表值参数关联的表类型的列元数据。 在这种情况下，在调用 SQLColumns 之前，必须将SQL_SOPT_SS_NAME_SCOPE设置为SQL_SS_NAME_SCOPE_TABLE_TYPE。 在应用程序检索完表值参数列元数据之后，应将 SQL_SOPT_SS_NAME_SCOPE 设置回原来的默认值 SQL_SS_NAME_SCOPE_TABLE。  
  
 也可以将 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 用于 CLR 用户定义类型参数。  
  
 无法获取非存储过程调用的准备的语句的表值参数元数据。 如果试图这样做，应用程序将返回错误代码为 SQLSTATE 42000 的 SQL_ERROR，以及消息“语法错误或访问冲突”。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
