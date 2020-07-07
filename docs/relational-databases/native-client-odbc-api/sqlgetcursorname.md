---
title: SQLGetCursorName |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 239113fdcd26521318979ad0fbd654801c827d3f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003483"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  如果应用程序未指定游标名称，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驱动程序会在游标生成时为应用程序生成一个游标名称。 应用程序可以使用**SQLGetCursorName**来检索用于定位的 UPDATE 和 DELETE 语句的驱动程序定义的游标名称。 应用程序无需调用**SQLSetCursorName**来利用定位的数据操作语句。  
  
## <a name="see-also"></a>另请参阅  
 [SQLGetCursorName 函数](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
