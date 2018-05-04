---
title: 使用语句参数 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- ODBC, parameters
- statements [ODBC], parameters
- parameter markers [ODBC]
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
ms.assetid: 2427d886-ec6c-49d7-b0b6-0d998b64cdb9
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 63a6181a3d62ebfb311264343b576b314dad5b2b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-statement-parameters"></a>使用语句参数
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  参数在 SQL 语句中是一种变量，它使 ODBC 应用程序能够：  
  
-   有效地为表中的列提供值。  
  
-   在构造查询条件时增强用户交互。  
  
-   管理**文本**， **ntext**，和**映像**数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-特定 C 数据类型。  
  
 例如，**部件**表具有名为的列**PartID**，**说明**，和**价格**。 若要添加不带参数的部分，需要构造 SQL 语句，例如：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 尽管使用已知的值集插入一行时可接受此语句，但要求应用程序插入多行时使用此语句会很不适合。 ODBC 可通过使应用程序将 SQL 语句中的任何数据值替换为参数标记来解决此问题。 这种参数标记由问号 (?) 表示。 在下面的示例中，三个数据值被替换为参数标记：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 参数标记然后被绑定到应用程序变量。 若要插入新行，应用程序只需设置变量的值并执行此语句。 然后，驱动程序检索变量的当前值并将其发送至数据源。 如果多次执行此语句，则应用程序可通过准备此语句使该进程更加有效。  
  
 每个参数标记均按从左到右的顺序由其分配至参数的序号引用。 在 SQL 语句中，最左侧的参数标记的序号值为 1；下一个的序号为 2，以此类推。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [绑定参数](../../relational-databases/native-client-odbc-queries/using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>另请参阅  
 [执行查询&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
