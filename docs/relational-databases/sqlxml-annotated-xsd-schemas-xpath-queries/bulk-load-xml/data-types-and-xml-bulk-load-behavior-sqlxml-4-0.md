---
title: 数据类型和 XML 大容量加载行为（SQLXML）
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 33619d0d3e1ec5d6684e3dc300317b1cc3666e79
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "75246734"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>数据类型和 XML 大容量加载行为 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  通常会忽略在映射架构（XSD 或 XDR 类型和**sql： datatype**）中指定的数据类型，但在以下情况下除外：  
  
 在 XSD 中：  
  
-   如果类型为**日期时间**或**时间**，则必须指定**SQL： Datatype** ，因为 XML 大容量加载会在将数据发送给 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之前执行数据转换。  
  
-   如果要大容量加载到中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的**uniqueidentifier**类型列，并且 XSD 值是包含大括号（{和}）的 GUID，则必须指定**sql： datatype = "uniqueidentifier"** 才能在将值插入列之前删除大括号。 如果未指定**sql： datatype** ，将用大括号发送该值，并且插入操作将失败。  
  
 有关**sql： datatype**的详细信息，请参阅[数据类型强制转换和 Sql： DATATYPE 批注 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 在 XDR 中：  
  
-   如果**dt： type**为**datetime**、 **time**、 **dateTime.tz**或**time.tz**，则必须指定**DT： Type**和**sql： datatype**数据类型，因为 XML 大容量加载在将数据发送到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之前会执行数据转换。  
  
-   如果 XML 数据的类型为**uuid**，则必须指定**sql： datatype** ;**dt： type = "uuid"** 也是必需的，除非数据是字符串数据。 如果未指定**dt： uuid**，XML 大容量加载将接受带大括号的字符串（如果需要，将其删除）。  
  
-   如果 XML 数据为**bin**或**bin**，则必须指定带有**dt： type**的 xml 数据类型。 XML 大容量加载然后将数据以十六进制形式加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
  
