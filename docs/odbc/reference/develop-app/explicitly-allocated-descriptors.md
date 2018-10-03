---
title: 显式分配描述符 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fbec69e0d984d843abc2b8754e111a1199c79a5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644535"
---
# <a name="explicitly-allocated-descriptors"></a>显式分配的描述符
应用程序可以显式分配应用程序描述符上随时连接到数据库的连接。 通过指定语句的特性处理使用该描述符句柄**SQLSetStmtAttr**，应用程序指示要使用该描述符来代替相应的驱动程序隐式分配应用程序描述符。 应用程序不能指定备用实现描述符。  
  
 应用程序可以将显式分配的描述符与多个语句相关联。 仅当应用程序实际连接到数据库时，才可以将描述符可以是显式分配的描述符。 应用程序可以通过释放其连接释放此类描述符显式或隐式。
