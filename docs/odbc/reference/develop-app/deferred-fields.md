---
title: 延迟的字段 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 094aba353e10ed568e1959b1d655109296507dee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305968"
---
# <a name="deferred-fields"></a>延迟的字段
如果设置了*延迟字段*的值，则不会使用这些值，但驱动程序会保存变量的地址以获得延迟的效果。 对于应用程序参数描述符，驱动程序将在调用**SQLExecDirect**或**SQLExecute**时使用变量的内容。 对于应用程序行描述符，驱动程序会在提取时使用变量的内容。  
  
 下面是延迟的字段：  
  
-   描述符记录的 SQL_DESC_DATA_PTR 和 SQL_DESC_INDICATOR_PTR 字段。  
  
-   应用程序描述符记录的 SQL_DESC_OCTET_LENGTH_PTR 字段。  
  
-   对于多行提取，描述符标头的 SQL_DESC_ARRAY_STATUS_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR 字段。  
  
 分配描述符后，每个描述符记录的延迟字段最初都具有 null 值。 Null 值的含义如下：  
  
-   如果 SQL_DESC_ARRAY_STATUS_PTR 的值为 null，多行提取将无法返回每行诊断信息的此组件。  
  
-   如果 SQL_DESC_DATA_PTR 具有 null 值，则该记录将解除绑定。  
  
-   如果 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 字段包含 null 值，则驱动程序将不返回该列的长度信息。  
  
-   如果 APD 的 SQL_DESC_OCTET_LENGTH_PTR 字段的值为 null，并且该参数是一个字符串，则驱动程序将假定该字符串以 null 结尾。 对于输出动态参数，此字段中的 null 值可防止驱动程序返回长度信息。 （如果 SQL_DESC_TYPE 字段未指示字符字符串参数，则忽略 SQL_DESC_OCTET_LENGTH_PTR 字段。）  
  
 应用程序在将其与字段相关联，并且驱动程序读取或写入它们的时间之间，不能解除分配或放弃延迟字段使用的变量。
