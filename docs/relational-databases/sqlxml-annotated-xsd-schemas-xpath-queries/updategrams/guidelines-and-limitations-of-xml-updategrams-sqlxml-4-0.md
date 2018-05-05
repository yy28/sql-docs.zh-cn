---
title: 指导原则和限制的 XML Updategram (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9dda62acddf1dbda2fe37c4ed458c37f5725ffdd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML Updategram 的指导原则和限制 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在使用 XML updategram 时，请记住以下事项：  
  
-   如果用于配合一对的插入操作属的 updategram **\<之前 >** 和**\<后 >** 块， **\<之前>** 块，则可以省略。 相反，如果删除操作， **\<后 >** 块，则可以省略。  
  
-   如果你具有多个使用属的 updategram **\<之前 >** 和**\<后 >** 块以**\<同步 >** 标记，同时**\<之前 >** 块和**\<后 >** 块必须指定到窗体**\<之前 >** 和**\<后 >** 对。  
  
-   updategram 中的更新适用于 XML 架构提供的 XML 视图。 因此，为使默认映射成功，必须在 updategram 中指定架构文件名；或者，如果未提供文件名，则元素名称和属性名称必须匹配数据库中的表名和列名。  
  
-   SQLXML 4.0 要求 updategram 中的所有列值都必须显式映射在提供的架构（XDR 或 XSD）中，以便为其子元素编写 XML 视图。 此行为不同于早期版本的 SQLXML，这允许未映射架构中，如果它已隐含的中的外键的一部分的列的值**sql:relationship**批注。 请注意，这一变化并不影响主键值传播到子元素，如果没有为子元素显式指定值，则对于 SQLXML 4.0，主键值仍会传播到子元素。  
  
-   如果你使用属的 updategram 来修改二进制列中的数据 (如[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**映像**数据类型)，你必须提供映射架构中的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型 (例如， **sql: datatype ="映像"**) 和 XML 数据类型 (例如， **dt: type ="binhex"** 或**dt: type ="binbase64**) 必须指定。 必须在属的 updategram; 中指定的二进制列的数据**sql:url-编码**映射架构中指定的批注将属的 updategram 被忽略。  
  
-   当你正在编写一个 XSD 架构，如果你为指定的值**sql:relation**或**sql:field**批注包含一个特殊字符，例如空格字符 （例如，在"订单详细信息"表名称），此值必须括在括号中 （例如，"[订单详细信息]"）。  
  
-   在使用 updategram 时，不支持链关系。 例如，如果表 A 和 C 通过使用表 B 的链关系相关，则在尝试运行和执行 updategram 时将发生以下错误：  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     即使架构和 updategram 均正确并且有效建立，但如果存在某一链关系，此错误仍将发生。  
  
-   Updategram 不允许传递的**映像**类型作为参数的数据，在更新过程。  
  
-   二进制大型对象 (BLOB) 类型类似**文本/ntext**和映像不应在**\<之前 >** 时阻止使用 updategram，因为这会将其包含在中使用并发控制。 由于 BLOB 类型的比较限制，这可能导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 出现问题。 例如，一 LIKE 关键字的 WHERE 子句中使用，用于比较的各个栏之间时**文本**数据类型; 但是，比较将失败，对于数据的大小大于 8 K 的 BLOB 类型。  
  
-   中的特殊字符**ntext**数据会导致问题，SQLXML 4.0 由于上用于 BLOB 类型的比较的限制。 例如，使用"[Serializable]"中的**\<之前 >** updategram 时并发检查的列中使用的块**ntext**类型会因以下 SQLOLEDB错误说明：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [属的 Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
