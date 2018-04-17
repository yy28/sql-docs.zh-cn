---
title: SQLGetTypeInfo （文本文件驱动程序） |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4b84e9e826eb2ad3104f00d9d39224fb2da6303
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo （文本文件驱动程序）
> [!NOTE]  
>  本主题提供文本文件特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 生成的表中返回的类型 (TYPE_NAME) 名称**SQLGetTypeInfo**将是最常使用的数据源的名称。  
  
 SQL_ALL_EXCEPT_LIKE 将返回可搜索的列中的字节，计数器、 双精度型、 单、 long 类型的值和短数据类型。 （如功能可以通过将值转换为使用 ODBC 规范的转换函数，然后执行比较的字符。）  
  
 当使用文本驱动程序时， **SQLGetTypeInfo**返回数据类型 （CHAR 和 LONGCHAR） 的文本 CASE_SENSITIVE 值为 FALSE 时的数据类型实际是区分大小写。
