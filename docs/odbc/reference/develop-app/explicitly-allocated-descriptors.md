---
title: 显式分配的描述符 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9950bc23a1e75606316039e6c2d66f3dba59940
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305688"
---
# <a name="explicitly-allocated-descriptors"></a>显式分配的描述符
应用程序可以在连接到数据库的任何时候在连接上显式分配应用程序描述符。 通过将描述符句柄指定为使用**SQLSetStmtAttr**的语句句柄的属性，应用程序指示驱动程序使用该描述符代替相应的隐式分配的应用程序描述符。 应用程序无法指定备用实现描述符。  
  
 应用程序可以将显式分配的描述符与多个语句相关联。 只有当应用程序实际连接到数据库时，描述符才能是显式分配的描述符。 应用程序可以显式释放此类描述符，也可以通过释放其连接来隐式释放。
