---
title: 数据类型和 XML 大容量加载行为 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ce59362d28c4d65e32834fd965cf710f49edb501
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274673"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>数据类型和 XML 大容量加载行为 (SQLXML 4.0)
  一般忽略在映射架构中指定的数据类型（XSD 或 XDR 类型以及 `sql:datatype`），但是以下情况除外：  
  
 在 XSD 中：  
  
-   如果类型为 `dateTime` 或 `time`，必须指定 `sql:datatype`，因为 XML 大容量加载在将数据发送到 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 前会执行数据转换。  
  
-   当进行大容量加载的列`uniqueidentifier`中键入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]XSD 值是一个 GUID，包括大括号 （{和}），您必须指定**sql: datatype ="uniqueidentifier"** 以在之前的值是删除大括号插入到的列。 如果未指定 `sql:datatype`，将发送包含大括号的值并且插入失败。  
  
 有关详细信息`sql:datatype`，请参阅[数据类型强制转换和 sql: datatype 批注&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 在 XDR 中：  
  
-   如果 `dt:type` 为 `datetime`、`time`、`dateTime.tz` 或 `time.tz`，必须同时指定 `dt:type` 和 `sql:datatype` 数据类型，因为 XML 大容量加载在将数据发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 前会执行数据转换。  
  
-   如果您的 XML 数据的类型`uuid`，`sql:datatype`必须指定;**dt: type ="uuid"** 也是必需的如果数据不是字符串数据。 如果未指定 `dt:uuid`，XML 大容量加载将接受包含大括号的字符串（并根据需要删除大括号）。  
  
-   如果 XML 数据为 `bin.base64` 或 `bin.hex`，必须使用 `dt:type` 指定 XML 数据类型。 XML 大容量加载然后将数据以十六进制形式加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
  
