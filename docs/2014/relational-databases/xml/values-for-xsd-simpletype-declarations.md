---
title: '&lt;xsd:simpleType&gt; 声明的值 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- xsd:simpleType declarations
ms.assetid: 557b972d-3af9-40bf-8382-72b05c9de1c1
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 14423da54a9890c7c286f5f997580f49931d1934
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290313"
---
# <a name="values-for-ltxsdsimpletypegt-declarations"></a>&lt;xsd:simpleType&gt; 声明的值
  下表根据所有已知的 XSD 简单类型枚举概述了已应用的限制。  
  
 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持在 **\<xsd:simpleType>** 声明中使用 NaN 值。 服务器拒绝包含 NaN 值的架构。  
  
|简单类型|限制|  
|-----------------|----------------|  
|`duration`|年份部分必须在-2 的范围内<sup>^</sup>31 到 2<sup>^</sup>31-1。 月、日、小时、分钟和秒都必须在 0 到 9999 范围内。 秒部分在小数点右侧有额外的三位精度。|  
|`dateTime`|时区子字段中的小时部分必须在 -14 到 +14 的可接受范围内。 年份部分必须在 1 到 9999 范围内。 月部分必须在 1 到 12 范围内。 日部分必须在 1 到 31 范围内且必须为有效的日历日期。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可检测出无效日期（如 1974-02-31，因为二月份没有 31 天），并返回错误。<br /><br /> 秒部分支持 100 纳秒的精度。 时区指示是可选的。<br /><br /> SQL Server 2005 支持的年范围是 -9999 到 9999。 现在，SQL Server 支持的年范围具有更强的限制性。 有关详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](compare-typed-xml-to-untyped-xml.md)。|  
|`date`|年份部分必须在 1 到 9999 范围内。 月部分必须在 1 到 12 范围内。 日部分必须在 1 到 31 范围内且必须为有效的日历日期。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可检测出无效日期（如 1974-02-31，因为二月份没有 31 天），并返回错误。<br /><br /> SQL Server 2005 支持的年范围是 -9999 到 9999。 现在，SQL Server 支持的年范围具有更强的限制性。 有关详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](compare-typed-xml-to-untyped-xml.md)。|  
|`gYearMonth`|年份部分必须在 -9999 到 9999 范围内。|  
|`gYear`|年份部分必须在 -9999 到 9999 范围内。|  
|`gMonthDay`|月部分必须在 1 到 12 范围内。 日部分必须在 1 到 31 范围内。|  
|`gDay`|日部分必须在 1 到 31 范围内。|  
|`gMonth`|月部分必须在 1 到 12 范围内。|  
|`decimal`|此类型的值必须符合 SQL 数值类型的格式。 此类型在内部表示支持总共包含最多 38 位的数字，其中 10 个数位留作小数精度。|  
|`float`|此类型的值必须符合 SQL `real` 类型的格式。|  
|**double**|此类型的值必须符合 SQL `float` 类型的格式。|  
|`string`|此类型的值必须符合 SQL `nvarchar(max)` 类型的格式。|  
|`anyURI`|此类型的值的长度不能多于 4000 个 Unicode 字符。|  
  
## <a name="see-also"></a>请参阅  
 [在服务器上使用 XML 架构集合的要求和限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
