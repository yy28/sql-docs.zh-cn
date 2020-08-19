---
description: 标准网关
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 687097813d01b27ac49e657f11a2b763e2ca1214
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448897"
---
# <a name="standard-gateway"></a>标准网关
*网关*是一种软件，它使一个 DBMS 看上去像另一个 DBMS。 也就是说，网关接受单个 DBMS 的编程接口、SQL 语法和数据流协议，并将其转换为隐藏 DBMS 的编程接口、SQL 语法和数据流协议。 例如，使用 Microsoft® SQL Server™编写的应用程序还可以通过微 Decisionware DB2 网关访问 DB2 数据;此产品会使 DB2 看起来像 SQL Server。 使用网关时，必须为每个目标数据库写入不同的网关。  
  
 虽然网关受 Dbms 之间的体系结构差异的限制，但它们非常适合用于标准化。 但是，如果所有 Dbms 都要标准化单个 DBMS 的编程接口、SQL 语法和数据流协议，而其 DBMS 被选为标准， 当然，没有任何商业 DBMS 供应商可能同意在竞争对手的产品上实现标准化。 如果开发了标准编程接口、SQL 语法和数据流协议，则不需要网关。
