---
title: 将 XSD 数据类型映射到 XPath 数据类型 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e64d1119f80406c2865ed3ca4b147d5004688cdd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>将 XSD 数据类型映射到 XPath 数据类型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  当针对 XSD 架构执行 XPath 查询和 XSD 类型中指定**xsd:type**属性，XPath 使用指定在处理查询时的数据类型。  
  
 节点的 XPath 数据类型从架构中的 XSD 数据类型派生，如下表中所示。 （EmployeeID 节点用于演示目的。）  
  
|XSD 数据类型|XDR 数据类型|等效<br /><br /> XPath 数据类型|SQL Server<br /><br /> 使用的转换|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **hexBinary**|**InclusionThresholdSetting**<br /><br /> **bin.base64bin.hex**|**不适用**|InclusionThresholdSetting<br /><br /> EmployeeID|  
|**Boolean**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**Decimal、 整数、 浮点型、 字节、 短整数、 int、 long、 float、 double、 unsignedByte、 unsignedShort、 unsignedInt、 unsignedLong**|**版本号、 int、 float、 i1、 i2、 i4、 i8、 r4、 r8ui1、 ui2、 ui4、 ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**id、 idref、 idrefsentity、 实体、 表示法、 nmtoken 和 nmtokens，DateTime、 字符串、 AnyURI**|**id、 idref、 idrefsentity、 实体、 枚举、 表示法、 nmtoken、 nmtokens、 char、 dateTime、 dateTime.tz、 字符串、 uri、 uuid**|**字符串**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**不适用 （没有任何数据类型在 XPath，它等效于 fixed14.4 XDR 数据类型。）**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**字符串**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**字符串**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
