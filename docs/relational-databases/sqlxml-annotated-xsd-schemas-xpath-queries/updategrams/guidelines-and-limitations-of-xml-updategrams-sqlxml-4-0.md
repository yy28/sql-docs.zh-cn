---
title: XML Updategram (SQLXML 4.0) 的准则和限制 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8418e7c70e1776a792b1dad4d34ffbdbcd07bd2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841791"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML Updategram 的指导原则和限制 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在使用 XML updategram 时，请记住以下事项：  
  
-   如果将 updategram 用于只具有单对的插入操作**\<之前 >** 并**\<后 >** 块**\<之前>** 块可省略。 反之，在删除操作**\<后 >** 块可省略。  
  
-   如果具有多个使用 updategram **\<之前 >** 并**\<后 >** 中的块**\<同步 >** 标记，同时**\<之前 >** 块并**\<后 >** 块都必须指定到窗体**\<之前 >** 和**\<后 >** 对。  
  
-   updategram 中的更新适用于 XML 架构提供的 XML 视图。 因此，为使默认映射成功，必须在 updategram 中指定架构文件名；或者，如果未提供文件名，则元素名称和属性名称必须匹配数据库中的表名和列名。  
  
-   SQLXML 4.0 要求 updategram 中的所有列值都必须显式映射在提供的架构（XDR 或 XSD）中，以便为其子元素编写 XML 视图。 此行为不同于早期版本的 SQLXML，这允许未映射架构中，如果它表示为作为中的外键的一部分的列的值**sql: relationship**批注。 请注意，这一变化并不影响主键值传播到子元素，如果没有为子元素显式指定值，则对于 SQLXML 4.0，主键值仍会传播到子元素。  
  
-   如果使用 updategram 修改二进制列中的数据 (如[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**映像**数据类型)，必须提供映射架构[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型 (例如， **sql: datatype ="图像"**) 和 XML 数据类型 (例如， **dt: type ="binhex"** 或**dt: type ="binbase64**) 必须指定。 必须在 updategram 中; 中指定二进制列的数据**sql:url-编码**updategram 将忽略在映射架构中指定的批注。  
  
-   在您撰写 XSD 架构中，如果为指定值**sql: relation**或**sql: field**批注包含一个特殊字符，例如空格字符 （例如，在"Order Details"表名称），此值必须括在括号内 （例如"[Order Details]"）。  
  
-   在使用 updategram 时，不支持链关系。 例如，如果表 A 和 C 通过使用表 B 的链关系相关，则在尝试运行和执行 updategram 时将发生以下错误：  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     即使架构和 updategram 均正确并且有效建立，但如果存在某一链关系，此错误仍将发生。  
  
-   Updategram 不允许传递**图像**类型作为参数的数据，在更新过程。  
  
-   二进制大型对象 (BLOB) 类型等**text/ntext**和映像不应在**\<之前 >** 时阻止使用 updategram，因为这将使它们在中使用并发控制。 由于 BLOB 类型的比较限制，这可能导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 出现问题。 例如，LIKE 关键字用于在 WHERE 子句中的列之间的比较**文本**数据类型; 但是，比较将失败的数据大小大于 8k 的 BLOB 类型。  
  
-   中的特殊字符**ntext**数据可能由于 BLOB 类型的比较限制导致 SQLXML 4.0 出现问题。 例如，使用"[Serializable]"中的**\<之前 >** 块中执行并发检查的列使用时，如果在 updategram **ntext**类型会因以下 SQLOLEDB错误说明：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
