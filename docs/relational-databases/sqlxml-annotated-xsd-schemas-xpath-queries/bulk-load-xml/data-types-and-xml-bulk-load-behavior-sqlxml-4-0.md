---
title: 数据类型和 XML 大容量加载行为 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
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
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: eb6f8a64d48e6fa1336a4f56ca63b07873ee7168
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32967424"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>数据类型和 XML 大容量加载行为 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  映射架构中指定的数据类型 (XSD 或 XDR 类型和**sql: datatype**) 通常将被忽略，除非在以下情况下：  
  
 在 XSD 中：  
  
-   如果类型为**dateTime**或**时间**，必须指定**sql: datatype**因为 XML 大容量加载执行数据转换之前将数据发送到 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   当你插入的某个列的大容量加载**uniqueidentifier**键入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]和 XSD 值是一个 GUID，包括大括号 （{和}），你必须指定**sql: datatype ="uniqueidentifier"** 到列中插入值之前，请删除大括号。 如果**sql: datatype**未指定，用大括号中发送的值和插入操作失败。  
  
 有关详细信息**sql: datatype**，请参阅[数据类型强制和 sql: datatype 批注&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 在 XDR 中：  
  
-   如果**dt: type**是**datetime**，**时间**， **dateTime.tz**，或**time.tz**，则必须同时指定**dt: type**和**sql: datatype**数据类型，因为 XML 大容量加载之前它将数据发送到执行数据转换[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   如果您的 XML 数据的类型是**uuid**， **sql: datatype**必须指定。**dt: type ="uuid"** 也是必需的除非此数据是字符串数据。 如果不指定**dt:uuid**，XML 大容量加载接受用括号的字符串 （和删除它们，如果需要）。  
  
-   如果 XML 数据，则**bin.base64**或**bin.hex**，必须指定使用的 XML 数据类型**dt: type**。 XML 大容量加载然后将数据以十六进制形式加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
  
