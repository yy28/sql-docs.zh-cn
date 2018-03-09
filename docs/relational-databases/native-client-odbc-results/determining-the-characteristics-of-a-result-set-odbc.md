---
title: "确定结果的特征集 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], characteristics
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLDescribeCol function
- metadata [ODBC]
- SQLColAttribute function
- SQLNumResultCols function
ms.assetid: 90be414c-04b3-46c0-906b-ae7537989b7d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43b848d7a0987ac6573478159f14f2365d9ee97c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="determining-the-characteristics-of-a-result-set-odbc"></a>确定结果集的特征 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  元数据是描述其他数据的数据。 例如，结果集元数据描述结果集的特征，比如结果集中的列数、这些列的数据类型、其名称、精度和可为 Null 性。  
  
 ODBC 通过其目录 API 函数向应用程序提供元数据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序实现很多的 ODBC API 目录功能与相应对调用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目录过程。  
  
 应用程序需要大多数结果集操作的元数据。 例如，应用程序使用某列的数据类型来确定要将哪一种变量绑定到该列； 使用某字符列的字节长度来确定必须有多少空间才能显示该列的数据。 应用程序确定列的元数据的方式取决于应用程序的类型。  
  
 垂直应用程序通常使用预定义的表，并对这些表执行预定义的操作。 由于此类应用程序的结果集元数据甚至是在编写应用程序之前定义的，并且由开发人员控制，因此可以将它硬编码到应用程序中。 例如，如果在数据源中将顺序 ID 列定义为 4 字节整数，则应用程序可以始终将 4 字节整数绑定到该列。 如果元数据在应用程序中为硬编码，则对应用程序所用的表进行更改通常意味着要对应用程序代码进行更改。  
  
 在一般应用程序中，尤其是支持即席查询的应用程序中，通常直到运行时才知道应用程序所创建的结果集的元数据。  
  
 若要确定结果集的特征，应用程序可以调用：  
  
-   [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)以确定请求多少列返回。  
  
-   [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)或[SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)来描述结果集中的列。  
  
 设计得很好的应用程序在编写时会假定结果集是未知的，并使用这些函数返回的信息来绑定结果集中的列。 在准备或执行语句之后，应用程序可以在任何时候调用这些函数。 但是，为了获得最佳性能，应用程序应调用**SQLColAttribute**， **SQLDescribeCol**，和**SQLNumResultCols**执行某个语句之后。  
  
 可以对元数据进行多个并发调用。 ODBC 驱动程序可以在使用静态服务器游标时调用作为 ODBC 目录 API 实现基础的系统目录过程。 这使得应用程序可以同时处理对 ODBC 目录函数的多个调用。  
  
 如果某个应用程序多次使用一组特定的元数据，则该应用程序很有可能得益于以下操作：首次获得专用变量中的信息时就进行信息缓存。 这样可以防止以后为获取相同信息而调用 ODBC 目录函数，这种调用会强制驱动程序执行到服务器的往返操作。  
  
## <a name="see-also"></a>另请参阅  
 [处理结果 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
