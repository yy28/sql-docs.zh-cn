---
title: 已准备的语句的表值参数元数据 |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 47938373c0f40f00926d537842afeee000f36870
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703768"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>准备的语句的表值参数元数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  应用程序可以获得通过 SQLNumParams 和 SQLDescribeParam 已准备的过程调用的元数据。 对于表值参数， *DataTypePtr*设置为 SQL_SS_TABLE。 通过 SQL_CA_SS_TYPE_NAME、 SQL_CA_SS_CATALOG_NAME，和 SQL_CA_SS_SCHEMA_NAME SQLGetDescField 提供了其他元数据。  
  
 SQL_CA_SS_TYPE_NAME、 SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 可与 SQLColumns 获取表值参数与关联的表类型的列元数据。 在这种情况下，SQL_SOPT_SS_NAME_SCOPE 必须设置为 SQL_SS_NAME_SCOPE_TABLE_TYPE 调用 SQLColumns 之前。 在应用程序检索完表值参数列元数据之后，应将 SQL_SOPT_SS_NAME_SCOPE 设置回原来的默认值 SQL_SS_NAME_SCOPE_TABLE。  
  
 也可以将 SQL_CA_SS_TYPE_NAME、SQL_CA_SS_CATALOG_NAME 和 SQL_CA_SS_SCHEMA_NAME 用于 CLR 用户定义类型参数。  
  
 无法获取非存储过程调用的准备的语句的表值参数元数据。 如果试图这样做，应用程序将返回错误代码为 SQLSTATE 42000 的 SQL_ERROR，以及消息“语法错误或访问冲突”。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
