---
title: 标准网关 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67551845c0dd8c6a28c0c4bc1c50f54ee8232df1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280070"
---
# <a name="standard-gateway"></a>标准网关
*网关*是使一个 DBMS 看起来像另一个软件。 也就是说，网关接受单个 DBMS 的编程接口、SQL 语法和数据流协议，并将其转换为隐藏 DBMS 的编程接口、SQL 语法和数据流协议。 例如，编写用于使用 Microsoft ® SQL Server 的应用程序™还可以通过微决策软件 DB2 网关访问 DB2 数据;此产品使 DB2 看起来像 SQL 服务器。 使用网关时，必须为每个目标数据库编写不同的网关。  
  
 尽管网关受到 DBMS 之间体系结构差异的限制，但它们是标准化的良好候选者。 但是，如果所有 DBMS 都必须在单个 DBMS 的编程接口、SQL 语法和数据流协议上进行标准化，那么选择其 DBMS 作为标准？ 当然，没有商业 DBMS 供应商可能同意对竞争对手的产品进行标准化。 如果开发了标准编程接口、SQL 语法和数据流协议，则不需要网关。
