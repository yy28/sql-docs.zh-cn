---
title: 数据类型和 XML 大容量加载行为（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d2eb9af2b353760f5b195b95d6a9f9d5d1efc9b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013419"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>数据类型和 XML 大容量加载行为 (SQLXML 4.0)
  一般忽略在映射架构中指定的数据类型（XSD 或 XDR 类型以及 `sql:datatype`），但是以下情况除外：  
  
 在 XSD 中：  
  
-   如果类型为 `dateTime` 或 `time`，必须指定 `sql:datatype`，因为 XML 大容量加载在将数据发送到 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 前会执行数据转换。  
  
-   如果要大容量加载到`uniqueidentifier`类型的列中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，并且 XSD 值是包含大括号（{和}）的 GUID，则必须指定**sql： datatype = "uniqueidentifier"** 才能在将值插入列之前删除大括号。 如果未指定 `sql:datatype`，将发送包含大括号的值并且插入失败。  
  
 有关`sql:datatype`的详细信息，请参阅[数据类型强制转换和 Sql： DATATYPE 批注 &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 在 XDR 中：  
  
-   如果 `dt:type` 为 `datetime`、`time`、`dateTime.tz` 或 `time.tz`，必须同时指定 `dt:type` 和 `sql:datatype` 数据类型，因为 XML 大容量加载在将数据发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 前会执行数据转换。  
  
-   如果 XML 数据的类型`uuid`为， `sql:datatype`则必须指定;**dt： type = "uuid"** 也是必需的，除非数据是字符串数据。 如果未指定 `dt:uuid`，XML 大容量加载将接受包含大括号的字符串（并根据需要删除大括号）。  
  
-   如果 XML 数据为 `bin.base64` 或 `bin.hex`，必须使用 `dt:type` 指定 XML 数据类型。 XML 大容量加载然后将数据以十六进制形式加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
  
