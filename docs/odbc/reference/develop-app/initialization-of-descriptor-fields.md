---
title: 描述符字段的初始化 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ed6479a60f1d0695107c216b2f0c94a55f68ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300117"
---
# <a name="initialization-of-descriptor-fields"></a>描述符字段的初始化
分配应用程序行描述符时，其字段将接收[SQLSetDescField 中](../../../odbc/reference/syntax/sqlsetdescfield-function.md)指示的初始值。 SQL_DEFAULTSQL_DESC_TYPE字段的初始值。 这提供了数据库数据的标准处理，以便向应用程序演示。 应用程序可以通过设置描述符记录的字段来指定对数据的不同处理。  
  
 描述符标头中SQL_DESC_ARRAY_SIZE的初始值为 1。 应用程序可以修改此字段以启用多行提取。  
  
 默认值的概念对 IRD 的字段无效。 仅当存在与其关联的已准备或执行语句时，应用程序才能访问 IRD 的字段。  
  
 IPD 的某些字段仅在驱动程序自动填充 IPD 后定义。 如果没有，它们未定义。 这些字段SQL_DESC_CASE_SENSITIVE、SQL_DESC_FIXED_PREC_SCALE、SQL_DESC_TYPE_NAME、SQL_DESC_UNSIGNED 和SQL_DESC_LOCAL_TYPE_NAME。
