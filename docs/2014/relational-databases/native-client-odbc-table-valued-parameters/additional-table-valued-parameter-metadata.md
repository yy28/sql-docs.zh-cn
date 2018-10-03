---
title: 其他表值参数元数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), catalog functions to retrieve metadata
- table-valued parameters (ODBC), metadata
ms.assetid: 6c193188-5185-4373-9a0d-76cfc150c828
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7b9aea58b56308764f907f8cf54bf74bb0663c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141517"
---
# <a name="additional-table-valued-parameter-metadata"></a>其他表值参数的元数据
  若要检索表值参数的元数据，应用程序调用 SQLProcedureColumns。 对于表值参数，SQLProcedureColumns 返回的单个行。 两个附加[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-添加了特定列，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME，以提供与表值参数关联的表类型的架构和目录信息。 为了符合 ODBC 规范，SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 的显示位置位于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本中添加的所有驱动程序特定列之前，并位于 ODBC 自身委托的所有列之后。  
  
 下表列出了对表值参数非常重要的列。  
  
|列名|数据类型|值/注释|  
|-----------------|---------------|---------------------|  
|DATA_TYPE|Smallint（非 NULL）|SQL_SS_TABLE|  
|TYPE_NAME|WVarchar(128)（非 NULL）|表值参数的类型名称。|  
|COLUMN_SIZE|Integer|NULL|  
|BUFFER_LENGTH|Integer|0|  
|DECIMAL_DIGITS|Smallint|NULL|  
|NUM_PREC_RADIX|Smallint|NULL|  
|NULLABLE|Smallint（非 NULL）|SQL_NULLABLE|  
|REMARKS|Varchar|NULL|  
|COLUMN_DEF|WVarchar(4000)|NULL|  
|SQL_DATA_TYPE|Smallint（非 NULL）|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|Smallint|NULL|  
|CHAR_OCTET_LENGTH|Integer|NULL|  
|ORDINAL_POSITION|Integer（非 NULL）|参数的序号位置。|  
|IS_NULLABLE|Varchar|"YES"|  
|SS_TYPE_CATALOG_NAME|WVarchar(128)（非 NULL）|包含表值参数表类型的类型定义的目录。|  
|SS_TYPE_SCHEMA_NAME|WVarchar(128)（非 NULL）|包含表值参数表类型的类型定义的架构。|  
  
 WVarchar 列在 ODBC 规范中定义为 Varchar，但实际上在所有最新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驱动程序中作为 WVarchar 返回。 该更改是在向 ODBC 3.5 规范添加 Unicide 支持时执行的，但不能显式指出。  
  
 若要获取表值参数的其他元数据，应用程序使用目录函数 SQLColumns 和 SQLPrimaryKeys。 在针对表值参数调用这些函数之前，应用程序必须将语句属性 SQL_SOPT_SS_NAME_SCOPE 设置为 SQL_SS_NAME_SCOPE_TABLE_TYPE。 该值表示应用程序需要表类型的元数据，而不是实际表。 然后，应用程序将传递作为表值参数的 TYPE_NAME *TableName*参数。 与使用 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME *CatalogName*和*SchemaName*参数，分别以标识的目录和表值参数的架构。 在应用程序检索完表值参数的元数据之后，该应用程序必须将 SQL_SOPT_SS_NAME_SCOPE 设置回原来的默认值 SQL_SS_NAME_SCOPE_TABLE。  
  
 将 SQL_SOPT_SS_NAME_SCOPE 设置为 SQL_SS_NAME_SCOPE_TABLE 时，对链接服务器的查询将失败。 SQLColumns 或 SQLPrimaryKeys 对包含服务器组件的目录的调用将失败。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
