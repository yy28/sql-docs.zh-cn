---
title: "延迟字段 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 38967637f505191a5ff353c13b4ebfbbe08e615a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="deferred-fields"></a>延迟的字段
值*延迟字段*时设置，但该驱动程序将保存延迟影响的变量的地址不会使用。 应用程序参数描述符，驱动程序使用这些变量的内容在调用时**SQLExecDirect**或**SQLExecute**。 对于应用程序行描述符，驱动程序在提取时使用这些变量的内容。  
  
 以下是延迟的字段：  
  
-   描述符记录 SQL_DESC_DATA_PTR 和 SQL_DESC_INDICATOR_PTR 字段。  
  
-   应用程序描述符记录 SQL_DESC_OCTET_LENGTH_PTR 字段。  
  
-   对于多行提取，描述符标头的 SQL_DESC_ARRAY_STATUS_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR 字段。  
  
 如果分配的描述符，延迟的记录的字段的每个描述符实例最初具有 null 值。 Null 值的含义是，如下所示：  
  
-   如果 SQL_DESC_ARRAY_STATUS_PTR 具有 null 值，多行提取将失败，返回此组件的每个行的诊断信息。  
  
-   如果 SQL_DESC_DATA_PTR 具有 null 值，该记录将是未绑定。  
  
-   如果 ARD SQL_DESC_OCTET_LENGTH_PTR 字段具有 null 值，该驱动程序不返回该列的长度信息。  
  
-   如果 APD SQL_DESC_OCTET_LENGTH_PTR 字段具有 null 值，并且参数是一个字符串，该驱动程序假定字符串是以 null 结尾。 对于输出动态参数，此字段中的 null 值阻止驱动程序中返回长度信息。 （如果 SQL_DESC_TYPE 字段不指示字符串参数，SQL_DESC_OCTET_LENGTH_PTR 字段则忽略。）  
  
 应用程序不得解除分配或放弃用于延迟的字段，它将它们关联与的字段的时间和驱动程序读取或写入它们的时间之间的变量。
