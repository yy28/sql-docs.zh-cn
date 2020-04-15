---
title: SQLTable 特权 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7a77eb5ea151c3a85f2235f48bb03d0e98dd9ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291897"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLTable 特权**可以在静态游标上执行。 尝试在可提升的（键集驱动或动态）上执行**SQLTable 特权**，SQL_SUCCESS_WITH_INFO指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序通过接受*目录名称*参数的两部分名称 *（Linked_Server_Name.Catalog_Name*）支持报告链接服务器上的表的信息。  
  
## <a name="see-also"></a>另请参阅  
 [SQLTable 特权函数](https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [ODBC API 实现细节](~/relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
