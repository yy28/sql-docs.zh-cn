---
title: 延迟字段 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305968"
---
# <a name="deferred-fields"></a>延迟的字段
设置*延迟字段*时不使用这些值，但驱动程序会保存变量的地址以执行延迟效果。 对于应用程序参数描述符，驱动程序在调用**SQLExecDirect**或**SQLExecute**时使用变量的内容。 对于应用程序行描述符，驱动程序在提取时使用变量的内容。  
  
 以下是递延字段：  
  
-   描述符记录的SQL_DESC_DATA_PTR字段和SQL_DESC_INDICATOR_PTR字段。  
  
-   应用程序描述符记录的SQL_DESC_OCTET_LENGTH_PTR字段。  
  
-   在多行提取的情况下，SQL_DESC_ARRAY_STATUS_PTR和SQL_DESC_ROWS_PROCESSED_PTR描述符标头的字段。  
  
 分配描述符时，每个描述符记录的递延字段最初具有 null 值。 null 值的含义如下：  
  
-   如果SQL_DESC_ARRAY_STATUS_PTR值为空，则多行提取无法返回每行诊断信息的此组件。  
  
-   如果SQL_DESC_DATA_PTR为 null 值，则记录将未绑定。  
  
-   如果 ARD 的SQL_DESC_OCTET_LENGTH_PTR字段具有空值，则驱动程序不会返回该列的长度信息。  
  
-   如果 APD 的SQL_DESC_OCTET_LENGTH_PTR字段具有空值，并且参数是字符串，则驱动程序假定字符串为 null 终止。 对于输出动态参数，此字段中的空值可防止驱动程序返回长度信息。 （如果SQL_DESC_TYPE字段不指示字符字符串参数，则忽略SQL_DESC_OCTET_LENGTH_PTR字段。  
  
 应用程序不得在将延迟字段与字段关联到驱动程序读取或写入这些字段的时间之间解调或丢弃用于延迟字段的变量。
