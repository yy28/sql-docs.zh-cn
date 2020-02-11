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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d272a26558aa163f8168288f95da8036666b9277
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73786941"
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在**SQLEndTran**提交或回滚操作时，Native Client ODBC 驱动程序会关闭语句的关联游标。 服务器游标将关闭，除非它们是静态的。 当**SQLEndTran**提交或回滚操作时，语句的关联游标的行为取决于驱动程序特定的 ODBC 连接属性的值，SQL_COPT_SS_PRESERVE_CURSORS，由[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)设置。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran 函数](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
