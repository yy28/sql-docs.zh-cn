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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c7800e7da867b4eb0c34fa3feeba5edb2d41cd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049869"
---
# <a name="deferred-fields"></a>延迟的字段
值*延迟的字段*时设置，但该驱动程序将保存的延迟影响的变量的地址不使用。 为应用程序参数描述符，驱动程序使用的变量的内容时对调用**SQLExecDirect**或**SQLExecute**。 为应用程序行描述符，驱动程序在提取时使用的变量的内容。  
  
 以下是延迟的字段：  
  
-   描述符记录 SQL_DESC_DATA_PTR 和 SQL_DESC_INDICATOR_PTR 字段。  
  
-   应用程序描述符记录 SQL_DESC_OCTET_LENGTH_PTR 字段。  
  
-   对于多行提取，描述符标头的 SQL_DESC_ARRAY_STATUS_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR 字段。  
  
 当分配的描述符时，延迟的字段的每个描述符记录最初具有 null 值。 Null 值的含义如下所示：  
  
-   如果 SQL_DESC_ARRAY_STATUS_PTR 具有 null 值，多行提取将失败，返回此组件的每个行诊断信息。  
  
-   如果 SQL_DESC_DATA_PTR 具有 null 值，该记录为未绑定。  
  
-   如果 ARD SQL_DESC_OCTET_LENGTH_PTR 字段具有 null 值，该驱动程序不返回长度为该列的信息。  
  
-   如果 APD SQL_DESC_OCTET_LENGTH_PTR 字段具有 null 值和参数是一个字符串，该驱动程序假定字符串是以 null 结尾。 对于输出动态参数，此字段中的 null 值可防止驱动程序返回长度的信息。 （如果 SQL_DESC_TYPE 字段并不表示的字符字符串参数，SQL_DESC_OCTET_LENGTH_PTR 字段则忽略。）  
  
 应用程序必须不解除分配或放弃使用延迟的字段，它将它们关联的字段的时间和驱动程序读取或写入它们的时间之间的变量。
