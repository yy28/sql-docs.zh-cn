---
title: SQL 程序 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 14ff76504c9a36657be60ba4855cf252474071d7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302354"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程都返回值。 **SQL过程**报告结果集列PROCEDURE_TYPESQL_PT_FUNCTION。  
  
 **SQL过程**返回SQL_SUCCESS*目录名称、架构名称*或*ProcName*参数是否存在值。 当在这些参数中使用无效值时 **，SQLFetch**将返回SQL_NO_DATA。  
  
 **SQL 过程**可以在静态服务器游标上执行。 尝试在可上升（动态或键集）游标上执行**SQL 过程**将返回SQL_SUCCESS_WITH_INFO，指示游标类型已更改。  
  
 **SQL程序**返回有关名称与*ProcName*匹配且可以由当前用户执行或当前用户已被授予"查看定义"权限的任何过程的信息。  
  
## <a name="see-also"></a>另请参阅  
 [SQL程序函数](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
