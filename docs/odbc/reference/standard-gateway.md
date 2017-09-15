---
title: "标准网关 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9375bc6bf5054bdfeddd4fc5e53a1494d74eb88b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="standard-gateway"></a>标准网关
A*网关*是一种软件导致如下所示另一个 DBMS。 即网关接受的编程接口，SQL 语法和数据流式传输协议的单个 DBMS 和将其转换到的编程接口，SQL 语法和数据流的隐藏 DBMS 的协议。 例如，编写用于 Microsoft® SQL Server™ 的应用程序可以还访问 DB2 数据通过 Micro Decisionware DB2 网关;此产品将导致 DB2 为类似于 SQL Server。 当使用网关时，必须为每个目标数据库编写不同的网关。  
  
 尽管网关会受到 Dbms 之间的体系结构差异，但它们都适合进行标准化。 但是，如果所有 Dbms 的编程接口上标准化，SQL 语法和数据将数据流的单个 DBMS，其 DBMS 是被选择作为标准的协议？ 当然任何商业 DBMS 供应商都不很可能以同意标准化竞争对手的产品。 如果开发标准编程接口、 SQL 语法和数据流协议，需没有网关。
