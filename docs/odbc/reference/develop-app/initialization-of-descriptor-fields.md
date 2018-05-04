---
title: 初始化描述符字段 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1875f69e3ba26a331b5042ebcdaaa803559f772a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="initialization-of-descriptor-fields"></a>描述符字段的初始化
中所示，其字段分配应用程序行描述符后，接收初始值[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 SQL_DESC_TYPE 字段的初始值是 SQL_DEFAULT。 这提供有关对应用程序的演示文稿的数据库数据的标准解决方法。 应用程序可以通过设置描述符记录的字段来指定不同的数据的处理。  
  
 描述符标头中的 SQL_DESC_ARRAY_SIZE 初始值为 1。 应用程序可以修改此字段可启用多行提取。  
  
 默认值的概念 IRD 字段无效。 只有在没有与之关联的已准备或执行语句时，应用程序可以获得对 IRD 的字段的访问。  
  
 仅在由驱动程序自动填充了 IPD 后定义 IPD 某些字段。 如果不是，它们是未定义。 这些字段是 SQL_DESC_CASE_SENSITIVE、 SQL_DESC_FIXED_PREC_SCALE、 SQL_DESC_TYPE_NAME、 SQL_DESC_UNSIGNED 和 SQL_DESC_LOCAL_TYPE_NAME。
