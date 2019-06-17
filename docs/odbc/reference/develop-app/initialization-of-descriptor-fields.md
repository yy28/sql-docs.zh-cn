---
title: 描述符字段的初始化 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d988099cad357254f04a79a8a6cccbbe4eb2768c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446808"
---
# <a name="initialization-of-descriptor-fields"></a>描述符字段的初始化
如下所示，其字段分配应用程序行描述符后，接收初始值[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 SQL_DESC_TYPE 字段的初始值是 SQL_DEFAULT。 这提供了有关标准处理以便为应用程序的数据库数据。 应用程序可以通过设置描述符记录的字段中指定数据处理的方式不同。  
  
 描述符标头中的 SQL_DESC_ARRAY_SIZE 初始值为 1。 应用程序可以修改此字段可启用多行提取。  
  
 默认值的概念并不的 IRD 字段有效。 只有在没有与之关联的已准备或执行语句时，应用程序能够访问的 IRD 字段。  
  
 只有在驱动程序会自动填充 IPD 后定义的 IPD 的某些字段。 如果不是，不进行定义。 这些字段是 SQL_DESC_CASE_SENSITIVE、 SQL_DESC_FIXED_PREC_SCALE、 SQL_DESC_TYPE_NAME、 SQL_DESC_UNSIGNED 和 SQL_DESC_LOCAL_TYPE_NAME。
