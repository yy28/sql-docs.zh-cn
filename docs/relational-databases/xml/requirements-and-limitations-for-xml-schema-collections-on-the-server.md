---
title: 在服务器上使用 XML 架构集合的要求和限制 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- identifiers [XML schema collections]
- XML schema collections [SQL Server], limitations
- substitution groups [XML in SQL Server]
- XML schema collections [SQL Server], guidelines
- lax validation
- enumeration facets [XML in SQL Server]
- decimal precision [XML in SQL Server]
- repeated XML schema collection values
- schema collections [SQL Server], limitations
- time zones [XML in SQL Server]
- precision decimals [XML in SQL Server]
- schema collections [SQL Server], guidelines
- lexical representation
ms.assetid: c2314fd5-4c6d-40cb-a128-07e532b40946
caps.latest.revision: 84
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cfece11f3cec121dcdd56a3918f3bdafc7bbd05e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="requirements-and-limitations-for-xml-schema-collections-on-the-server"></a>在服务器上使用 XML 架构集合的要求和限制
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  XML 架构定义语言 (XSD) 验证对使用 **xml** 数据类型的 SQL 列具有某些限制。 下表提供有关这些限制的详细信息，还提供了修改 XSD 架构的准则以使它可以与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一起使用。 本部分中的主题提供有关使用这些特定限制和准则的其他信息。  
  
|项|限制|  
|----------|----------------|  
|**minOccurs** 和 **maxOccurs**|**minOccurs** 和 **maxOccurs** 属性的值必须符合 4 字节整数。 服务器拒绝不符合的架构。|  
|**\<xsd:choice>**|如果架构中包含无子级的 **\<xsd:choice>** 粒子，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒绝该架构，除非该粒子的 **minOccurs** 属性值定义为零。|  
|**\<xsd:include>**|当前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持此元素。 服务器拒绝包含此元素的 XML 架构。<br /><br /> 一种解决方法是，可以预处理包括 **\<xsd:include>** 指令的 XML 架构，来复制所有包含的架构的内容并将其合并为单个架构，以上载到服务器。 有关详细信息，请参阅 [预处理架构以便合并包括的架构](../../relational-databases/xml/preprocess-a-schema-to-merge-included-schemas.md)。|  
|**\<xsd:key>**、**\<xsd:keyref>** 和 **\<xsd:unique>**|当前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持这些用于强制唯一性或建立键和键引用的基于 XSD 的约束。 无法注册包含这些元素的 XML 架构。|  
|**\<xsd:redefine>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持此元素。 有关更新架构的其他方法的信息，请参阅 [&lt;xsd: redefine&gt; 元素](../../relational-databases/xml/the-xsd-redefine-element.md)一起使用。|  
|**\<xsd:simpleType>** 值|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对带有除 **xs:time** 和 **xs:dateTime**以外的秒部分的简单类型仅支持毫秒精度，对 **xs:time** 和 **xs:dateTime**则支持 100 纳秒精度。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对所有已识别的 XSD 简单类型枚举具有限制。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持在 **\<xsd:simpleType>** 声明中使用“NaN”值。<br /><br /> 有关详细信息，请参阅[&lt;xsd:simpleType&gt; 声明的值](../../relational-databases/xml/values-for-xsd-simpletype-declarations.md)一起使用。|  
|**xsi:schemaLocation** 和 **xsi:noNamespaceSchemaLocation**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果在插入到 **xml** 数据类型的列或变量的 XML 实例数据中存在这些属性，则将忽略这些属性。|  
|**xs:QName**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持从 **xs:QName** 派生的使用 XML 架构限制元素的类型。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持将 **xs:QName** 作为成员元素的联合类型。<br /><br /> 有关详细信息，请参阅 [The xs:QName Type](../../relational-databases/xml/the-xs-qname-type.md)。|  
|将成员添加到现有替换组|无法将成员添加到 XML 架构集合中的现有替换组。 XML 架构中的替换组有以下限制：头元素和所有其成员元素必须在相同的 {CREATE | ALTER} XML SCHEMA COLLECTION 语句中定义。|  
|规范格式和模式限制|值的规范表示形式不能违反其类型的模式限制。 有关详细信息，请参阅 [Canonical Forms and Pattern Restrictions](../../relational-databases/xml/canonical-forms-and-pattern-restrictions.md)。|  
|枚举方面|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持包含以下类型的 XML 架构：具有模式方面或违反这些方面的枚举的类型。|  
|方面长度|**length**、 **minLength**和 **maxLength** 方面作为 **long** 类型存储。 此类型为 32 位类型。 因此，这些值的可接受值的范围是 2^31。|  
|ID 属性|每个 XML 架构组件可在其上具有 ID 属性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对 **ID** 类型的 **\<xsd:attribute>** 声明强制唯一性，但不存储这些值。 唯一性的强制的作用范围是 {CREATE | ALTER} XML SCHEMA COLLECTION 语句。|  
|ID 类型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持类型为 **xs:ID**、 **xs:IDREF**或 **xs:IDREFS**的元素。 架构不会声明这种类型的元素或者从这种类型的限制或扩展派生的元素。|  
|本地命名空间|必须为 **\<xsd:any>** 元素显式指定本地命名空间。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒绝使用空字符串 ("") 作为命名空间属性的值的架构。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而是要求显式使用“##local”以指示作为通配符实例的未限定元素或属性。|  
|混合类型和简单内容|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持将混合类型限制为简单内容。 有关详细信息，请参阅 [Mixed Type and Simple Content](../../relational-databases/xml/mixed-type-and-simple-content.md)。|  
|NOTATION 类型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持 NOTATION 类型。|  
|内存不足的情况|在使用大型 XML 架构集合时，可能会出现内存不足的情况。 有关此问题的解决方案，请参阅 [大型 XML 架构集合和内存不足的情况](../../relational-databases/xml/large-xml-schema-collections-and-out-of-memory-conditions.md)。|  
|重复的值|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒绝其中的 block 或 final 属性具有重复值（如“restriction restriction”和“extension extension”）的架构。|  
|架构组件标识符|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将架构组件的标识符限于最大长度为 1000 个 Unicode 字符。 另外，不支持在标识符中使用代理项字符对。|  
|时区信息|在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中，完全支持进行 XML 架构验证的 **xs:date**、 **xs:time**和 **xs:dateTime** 值的时区信息。 通过 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 向后兼容模式，始终将时区信息规范化为协调世界时（格林尼治标准时间）。 对于 **dateTime** 类型的元素，服务器将通过使用偏移值（“-05:00”）和返回相应的 GMT 时间转换提供给 GMT 的时间。|  
|联合类型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持联合类型的限制。|  
|可变精度小数|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持可变精度小数。 **xs:decimal** 类型表示任意精度十进制数字。 最小符合 XML 处理器必须支持最小值为 `totalDigits=18`的十进制数字。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持 `totalDigits=38,` ，但将小数位数限制为 10。 所有 **xs:decimal** 实例化的值均由服务器通过使用 SQL 类型数值 (38, 10) 在内部表示。|  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[Canonical Forms and Pattern Restrictions](../../relational-databases/xml/canonical-forms-and-pattern-restrictions.md)|说明规范格式和模式限制。|  
|[通配符组成部分和内容验证](../../relational-databases/xml/wildcard-components-and-content-validation.md)|介绍了使用通配符、宽松验证和任何带有 XML 架构集合的类型元素的限制。|  
|[&lt;xsd: redefine&gt; 元素](../../relational-databases/xml/the-xsd-redefine-element.md)|说明使用 \<xsd:redefine> 元素的限制并介绍了解决方法。|  
|[The xs:QName Type](../../relational-databases/xml/the-xs-qname-type.md)|介绍与 xs:QName 类型有关的限制。|  
|[&lt;xsd:simpleType&gt; 声明的值](../../relational-databases/xml/values-for-xsd-simpletype-declarations.md)|介绍了对 \<xsd:simpleType> 声明适用的限制。|  
|[Enumeration Facets](../../relational-databases/xml/enumeration-facets.md)|介绍与枚举方面有关的限制。|  
|[Mixed Type and Simple Content](../../relational-databases/xml/mixed-type-and-simple-content.md)|介绍将混合类型限制为简单内容的限制。|  
|[大型 XML 架构集合和内存不足的情况](../../relational-databases/xml/large-xml-schema-collections-and-out-of-memory-conditions.md)|提供在大型架构集合有时发生内存不足时的解决方案。|  
|[不确定性内容模型](../../relational-databases/xml/non-deterministic-content-models.md)|介绍与不确定性内容模型有关的限制。|  
  
## <a name="see-also"></a>另请参阅  
 [XML 数据 (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)   
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [授予对 XML 架构集合的权限](../../relational-databases/xml/grant-permissions-on-an-xml-schema-collection.md)   
 [唯一粒子归属约束](../../relational-databases/xml/unique-particle-attribution-constraint.md)   
 [XML 架构集合 (SQL Server)](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
