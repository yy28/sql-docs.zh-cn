---
title: 显式分配的描述符 |Microsoft Docs
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
ms.openlocfilehash: 5808265a9ab70b9947cea64fef790497c7229da8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069932"
---
# <a name="explicitly-allocated-descriptors"></a>显式分配的描述符
应用程序可以在连接到数据库时，在该连接上显式分配应用程序描述符。 通过使用**SQLSetStmtAttr**将该描述符句柄指定为语句句柄的属性，应用程序将指示该驱动程序使用该描述符来替换相应的隐式分配的应用程序描述符。 应用程序无法指定替代实现描述符。  
  
 应用程序可将显式分配的描述符与多个语句相关联。 仅当应用程序实际连接到数据库时，描述符才能是显式分配的描述符。 应用程序可以显式释放此类描述符，也可以通过释放其连接来隐式释放它。
