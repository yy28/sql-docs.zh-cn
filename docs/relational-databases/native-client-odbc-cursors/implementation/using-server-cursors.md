---
title: "使用服务器游标 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d6be8e988dfa7cc388544a215a333d6eb876bf7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="using-server-cursors"></a>使用服务器游标
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  如果 ODBC 应用程序将任何 ODBC 游标特性设置为默认值，以外的任何[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序会请求服务器以实现同一类型的 API 服务器游标。 如果使用 API 服务器游标，将在客户端上释放内存，并且可以大幅减少客户端与服务器之间的网络通信量。  
  
 API 服务器游标的潜在缺点是它们当前不支持所有 SQL 语句。 API 服务器游标无法用于执行：  
  
-   返回多个结果集的批处理或存储过程。  
  
-   包含 COMPUTE、COMPUTE BY、FOR BROWSE 或 INTO 子句的 SELECT 语句。  
  
-   引用远程存储过程的 EXECUTE 语句。  
  
 连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例时，如果使用服务器游标执行具有这些特征的语句，将导致游标转换到默认结果集。 连接到较早版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时，它将导致错误。  
  
## <a name="see-also"></a>另请参阅  
 [如何实现游标](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
