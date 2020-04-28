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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ed6479a60f1d0695107c216b2f0c94a55f68ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300117"
---
# <a name="initialization-of-descriptor-fields"></a>描述符字段的初始化
如果分配了应用程序行说明符，则其字段将接收[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中所示的初始值。 SQL_DESC_TYPE 字段的初始值为 SQL_DEFAULT。 这为显示到应用程序的数据库数据提供了标准处理。 应用程序通过设置描述符记录的字段，可以指定不同的数据处理方式。  
  
 描述符标头中 SQL_DESC_ARRAY_SIZE 的初始值为1。 应用程序可以修改此字段以启用多行提取。  
  
 默认值的概念对于 IRD 的字段无效。 仅当有一个已准备的或已执行的语句与其关联时，应用程序才可以访问 IRD 的字段。  
  
 只有在驱动程序自动填充 IPD 后，才会定义 IPD 的某些字段。 如果不是，则未定义。 这些字段为 SQL_DESC_CASE_SENSITIVE、SQL_DESC_FIXED_PREC_SCALE、SQL_DESC_TYPE_NAME、SQL_DESC_UNSIGNED 和 SQL_DESC_LOCAL_TYPE_NAME。
