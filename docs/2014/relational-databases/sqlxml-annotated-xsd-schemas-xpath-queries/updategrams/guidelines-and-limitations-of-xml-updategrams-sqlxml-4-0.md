---
title: XML Updategram (SQLXML 4.0) 的准则和限制 |Microsoft Docs
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
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ffd38da9c65154ba7bc2af70746416558f8aceea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150828"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML Updategram 的指导原则和限制 (SQLXML 4.0)
  在使用 XML updategram 时，请记住以下事项：  
  
-   如果将 updategram 用于只具有单对的插入操作**\<之前 >** 并**\<后 >** 块**\<之前>** 块可省略。 反之，在删除操作**\<后 >** 块可省略。  
  
-   如果具有多个使用 updategram **\<之前 >** 并**\<后 >** 中的块**\<同步 >** 标记，同时**\<之前 >** 块并**\<后 >** 块都必须指定到窗体**\<之前 >** 和**\<后 >** 对。  
  
-   updategram 中的更新适用于 XML 架构提供的 XML 视图。 因此，为使默认映射成功，必须在 updategram 中指定架构文件名；或者，如果未提供文件名，则元素名称和属性名称必须匹配数据库中的表名和列名。  
  
-   SQLXML 4.0 要求 updategram 中的所有列值都必须显式映射在提供的架构（XDR 或 XSD）中，以便为其子元素编写 XML 视图。 此行为不同于 SQLXML 的早期版本，这些版本允许架构中未映射的列值（如果它表示为 `sql:relationship` 批注中外键的一部分）。 请注意，这一变化并不影响主键值传播到子元素，如果没有为子元素显式指定值，则对于 SQLXML 4.0，主键值仍会传播到子元素。  
  
-   如果使用 updategram 修改二进制列中的数据 (如[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]`image`数据类型)，必须提供映射架构[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型 (例如， `sql:datatype="image"`) 和 XML 数据类型 (例如， `dt:type="binhex"`或`dt:type="binbase64`) 必须指定。 必须在 updategram 中指定二进制列的数据；updategram 将忽略在映射架构中指定的 `sql:url-encode` 批注。  
  
-   在您撰写某一 XSD 架构时，如果为 `sql:relation` 或 `sql:field` 批注指定的值包括特殊字符，例如空格字符（如“Order Details”表名称中的空格），则该值必须用括号括起来（例如“[Order Details]”）。  
  
-   在使用 updategram 时，不支持链关系。 例如，如果表 A 和 C 通过使用表 B 的链关系相关，则在尝试运行和执行 updategram 时将发生以下错误：  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     即使架构和 updategram 均正确并且有效建立，但如果存在某一链关系，此错误仍将发生。  
  
-   Updategram 不允许在更新期间将 `image` 类型数据作为参数传递。  
  
-   二进制大型对象 (BLOB) 类型等`text/ntext`和映像不应在**\<之前 >** 时阻止使用 updategram，因为这将使它们用在并发控制。 由于 BLOB 类型的比较限制，这可能导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 出现问题。 例如，在 WHERE 子句中使用 LIKE 关键字比较 `text` 数据类型的列；不过，对于数据大小大于 8K 的 BLOB 类型，比较将失败。  
  
-   由于 BLOB 类型的比较限制，`ntext` 数据中的特殊字符可能导致 SQLXML 4.0 出现问题。 例如，使用"[Serializable]"中的**\<之前 >** 块中执行并发检查的列使用时，如果在 updategram`ntext`类型时将失败并显示以下 SQLOLEDB 错误说明：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
