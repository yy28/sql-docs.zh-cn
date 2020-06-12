---
title: 将 XSD 数据类型映射到 XPath 数据类型（SQLXML）
description: 了解如何在 SQLXML 4.0 中执行 XPath 查询时，将 XSD 数据类型映射到 XPath 数据类型。
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1dd2800d89016223e172e11ebde2cc3f8332e7d4
ms.sourcegitcommit: 9921501952147b9ce3e85a1712495d5b3eb13e5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84215702"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>将 XSD 数据类型映射到 XPath 数据类型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  针对 XSD 架构执行 XPath 查询且 xsd 类型在**xsd： type**属性中指定时，xpath 使用在处理查询时指定的数据类型。  
  
 节点的 XPath 数据类型从架构中的 XSD 数据类型派生，如下表中所示。 （EmployeeID 节点用于演示目的。）  
  
|XSD 数据类型|XDR 数据类型|等效<br /><br /> XPath 数据类型|SQL Server<br /><br /> 使用的转换|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**无**<br /><br /> **base64bin**|**不适用**|无<br /><br /> EmployeeID|  
|**布尔值**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**Decimal、integer、float、byte、short、int、long、float、double、unsignedByte、unsignedShort、unsignedInt、unsignedLong**|**number、int、float、i1、i2、i4、i8、r4、r8、ui1、ui2、ui4、ui8**|**数字**|CONVERT(float(53), EmployeeID)|  
|**id、idref、idrefsentity、entities、notation、nmtoken、nmtokens、DateTime、string、AnyURI**|**id、idref、idrefsentity、实体、枚举、notation、nmtoken、nmtokens、char、dateTime、dateTime.tz、string、uri、uuid**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**不适用（在 XPath 中没有与 fixed14.4 XDR 数据类型等效的数据类型。）**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
