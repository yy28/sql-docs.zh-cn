---
title: SQLEndTran |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d0c7c7c56859786420d9986b40684bbec9d5445d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003576"
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在**SQLEndTran**提交或回滚操作时，Native Client ODBC 驱动程序会关闭语句的关联游标。 服务器游标将关闭，除非它们是静态的。 当**SQLEndTran**提交或回滚操作时，语句的关联游标的行为取决于驱动程序特定的 ODBC 连接属性的值，SQL_COPT_SS_PRESERVE_CURSORS，由[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)设置。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran 函数](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
