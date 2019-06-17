---
title: 标准网关 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c70a558b065765dd9f8c0895345959e8aa22ebfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232096"
---
# <a name="standard-gateway"></a>标准网关
一个*网关*是一种软件会导致一个 DBMS 与另一个类似的形式。 也就是说，网关接受编程接口，SQL 语法和数据流协议的单个 dbms 和将其转换到的编程接口，SQL 语法并数据流协议隐藏 DBMS。 例如，应用程序编写为使用 Microsoft® SQL Server™ 还可以访问 DB2 数据通过 Micro Decisionware DB2 网关;此产品将导致 DB2 看起来像 SQL Server。 当使用网关时，必须为每个目标数据库编写不同的网关。  
  
 尽管网关都受 Dbms 之间的体系结构差异，但它们是标准化的良好候选项。 但是，如果所有的 Dbms 的编程接口上实现标准化，SQL 语法和数据格式数据流协议的 DBMS 是被选为标准的单一 dbms？ 当然没有商业 DBMS 供应商很可能同意在竞争对手的产品上实现标准化。 而开发的标准编程接口、 SQL 语法和数据流协议，如果需要没有网关。
