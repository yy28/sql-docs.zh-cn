---
title: 类型化的 XML 与非类型化的 XML 的比较 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- xml data type [SQL Server], variables
- parameters [XML in SQL Server]
- facets [XML in SQL Server]
- xml data type [SQL Server], columns
- untyped XML
- xml data type [SQL Server], typed xml
- XML [SQL Server], typed
- variables [XML in SQL Server], creating
- xml data type [SQL Server], untyped xml
- columns [XML in SQL Server], creating
- typed XML
- document mode processing [SQL Server]
- XML [SQL Server], untyped
- xml data type [SQL Server], parameters
ms.assetid: 4bc50af9-2f7d-49df-bb01-854d080c72c7
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bcffb5fa9a023f893446479769c75089ca13fe06
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43890263"
---
# <a name="compare-typed-xml-to-untyped-xml"></a>类型化的 XML 与非类型化的 XML 的比较
  您可以创建 `xml` 类型的变量、参数和列。 （可选） 可以与变量、 参数或列关联的 XML 架构集合`xml`类型。 在这种情况下，`xml`数据类型实例称为*键入*。 否则，XML 实例称作“非类型化” 的实例。  
  
## <a name="well-formed-xml-and-the-xml-data-type"></a>格式正确的 XML 和 xml 数据类型  
 `xml` 数据类型可实现 ISO 标准的 `xml` 数据类型。 因此，它可以在非类型化的 XML 列中存储格式正确的 XML 1.0 版的文档以及具有文本节点和任意数量顶级元素的所谓的 XML 内容片段。 系统将检查数据格式是否正确，但不要求将列绑定到 XML 架构，并且拒绝在扩展意义上格式不正确的数据。 对于非类型化的 XML 变量和参数也是如此。  
  
## <a name="xml-schemas"></a>XML 架构  
 XML 架构提供以下信息：  
  
-   **验证约束。** 每当向类型化的 xml 实例赋值或修改这样的实例时，SQL Server 都将验证该实例。  
  
-   **数据类型信息。** 架构提供有关 `xml` 数据类型实例中属性和元素的类型的信息。 与非类型化的 `xml` 可以提供的操作语义相比，类型信息为实例中包含的值提供了更精确的操作语义。 例如，可以对十进制值执行十进制算术运算，而不能对字符串值执行十进制算术运算。 因此，与非类型化的 XML 相比，可以对类型化的 XML 存储进行更大程度的压缩。  
  
## <a name="choosing-typed-or-untyped-xml"></a>选择类型化或非类型化的 XML  
 使用非类型化`xml`在以下情况下的数据类型：  
  
-   您没有对应于您的 XML 数据的架构。  
  
-   您有架构，但不希望服务器验证数据。 当应用程序将数据存储到服务器之前会执行客户端验证时，临时存储对该架构而言无效的 XML 数据时，或在服务器上使用不支持的架构组件时，需要如此。  
  
 使用类型化`xml`在以下情况下的数据类型：  
  
-   您有对应于您的 XML 数据的架构，并且希望服务器根据 XML 架构验证您的 XML 数据。  
  
-   您希望利用基于类型信息的存储和查询优化。  
  
-   您希望在编译查询过程中更好地利用类型信息。  
  
 类型化的 XML 列、参数和变量可以存储 XML 文档或内容。 但是，在声明时必须使用标志指定是存储文档还是存储内容。 此外，必须提供 XML 架构集合。 如果每个 XML 实例都刚好有一个顶级元素，请指定 DOCUMENT。 否则，请使用 CONTENT。 查询编译器在查询编译期间的类型检查过程中使用 DOCUMENT 标志来推断单独的顶级元素。  
  
## <a name="creating-typed-xml"></a>创建类型化的 XML  
 您可以创建类型化之前`xml`变量、 参数或列，您必须先注册使用的 XML 架构集合[CREATE XML SCHEMA COLLECTION &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-xml-schema-collection-transact-sql)。 然后可以将 XML 架构集合关联的变量、 参数或列的`xml`数据类型。  
  
 在下列示例中，使用由两部分组成的名称命名约定指定 XML 架构集合名称。 第一部分是架构名称，第二部分是 XML 架构集合名称。  
  
### <a name="example-associating-a-schema-collection-with-an-xml-type-variable"></a>示例：将架构集合与 xml 类型变量关联起来  
 下面的示例创建`xml`类型变量并将架构集合与之相关联。 该示例中指定的架构集合已导入 **AdventureWorks** 数据库。  
  
```  
DECLARE @x xml (Production.ProductDescriptionSchemaCollection);   
```  
  
### <a name="example-specifying-a-schema-for-an-xml-type-column"></a>示例：为 xml 类型列指定架构  
 下面的示例创建具有表`xml`类型列和为列指定一个架构：  
  
```  
CREATE TABLE T1(  
 Col1 int,   
 Col2 xml (Production.ProductDescriptionSchemaCollection)) ;  
```  
  
### <a name="example-passing-an-xml-type-parameter-to-a-stored-procedure"></a>示例：将 xml 类型参数传递给存储过程  
 下面的示例传入`xml`类型到存储过程的参数和为该变量指定一个架构：  
  
```  
CREATE PROCEDURE SampleProc   
  @ProdDescription xml (Production.ProductDescriptionSchemaCollection)   
AS   
...  
```  
  
 注意有关 XML 架构集合的以下事项：  
  
-   XML 架构集合只有在通过 [创建 XML 架构集合](/sql/t-sql/statements/create-xml-schema-collection-transact-sql)注册该集合的数据库中才可用。  
  
-   如果从字符串转换为类型化`xml`数据类型，分析也执行验证，键入，根据指定的集合中的 XML 架构命名空间。  
  
-   可以从类型化的 `xml` 数据类型转换到非类型化的 `xml` 数据类型，反之亦然。  
  
 有关在 SQL Server 中生成 XML 的其他方法的详细信息，请参阅 [创建 XML 数据的实例](create-instances-of-xml-data.md)。 生成 XML 后，它可以赋给`xml`数据类型变量中存储`xml`类型以进行其他处理的列。  
  
 数据类型层次结构中`xml`如下所示的数据类型`sql_variant`和用户定义类型，但所有内置类型之上。  
  
### <a name="example-specifying-facets-to-constrain-a-typed-xml-column"></a>示例：指定用于约束类型化的 xml 列的方面  
 对于类型化`xml`列，您可以限制以允许存储在其中每个实例只将单个顶级元素的列。 可以在创建了表以后通过指定可选的 `DOCUMENT` 方面来进行此操作，如以下示例中所示：  
  
```  
CREATE TABLE T(Col1 xml   
   (DOCUMENT Production.ProductDescriptionSchemaCollection));  
GO  
DROP TABLE T;  
GO  
```  
  
 默认情况下，实例存储在类型化`xml`列存储为 XML 内容而不是 XML 文档。 这允许存储以下内容：  
  
-   零个或多个顶级元素  
  
-   顶级元素中的文本节点  
  
 还可以通过添加 `CONTENT` 方面显式指定此行为，如以下示例中所示：  
  
```  
CREATE TABLE T(Col1 xml(CONTENT Production.ProductDescriptionSchemaCollection));  
GO -- Default  
```  
  
 请注意，可以在定义 `xml` 类型（类型化的 xml）的任何位置指定可选的 DOCUMENT/CONTENT 方面。 例如，当创建类型化`xml`变量时，可以添加 DOCUMENT/CONTENT 方面，如在下面的示例所示：  
  
```  
declare @x xml (DOCUMENT Production.ProductDescriptionSchemaCollection);  
```  
  
## <a name="document-type-definition-dtd"></a>文档类型定义 (DTD)  
 可以使用 XML 架构类型化 `xml` 数据类型列、变量和参数，但不可使用 DTD 类型化它们。 但是，内联 DTD 既可用于非类型化的 XML，也可用于类型化的 XML，以便提供默认值，并将实体引用替换为其扩展形式。  
  
 可以通过使用第三方工具将 DTD 转换为 XML 架构文档，然后将 XML 架构加载到数据库中。  
  
## <a name="upgrading-typed-xml-from-sql-server-2005"></a>从 SQL Server 2005 升级类型化 XML  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 对 XML 架构支持（包括对宽松验证的支持）进行了多项扩展，改进了对 **xs:date**、 **xs:time** 和 **xs:dateTime** 实例数据的处理，并新增了对列表和联合类型的支持。 大多数情况下，这些更改不会影响升级过程。 但是，如果你使用了 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中允许使用 **xs:date**、 **xs:time**或 **xs:dateTime** （或任何子类型）类型的值的 XML 架构集合，则在将 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库附加到更高版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时将执行以下升级步骤：  
  
1.  对于每个 XML 列，如果该列是使用包含特定元素或属性（这些元素或属性被类型化为 **xs:anyType**、 **xs:anySimpleType**、 **xs:date** 或其任何子类型、 **xs:time** 或其任何子类型、 **xs:dateTime** 或其任何子类型，或者属于包含上述任何类型的联合类型或列表类型）的 XML 架构集合进行类型化的，将会执行以下操作：  
  
    1.  将禁用该列的所有 XML 索引。  
  
    2.  将继续采用 Z 时区表示所有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 值，这是因为已针对 Z 时区将这些值规范化。  
  
    3.  任何小于元年 1 月 1 日的 **xs:date** 或 **xs:dateTime** 值在重新生成索引或对包含该值的 XML 数据类型执行 XQuery 或 XML-DML 语句时都将导致运行时错误。  
  
2.  **xs:date** 或 **xs:dateTime** 方面中的任何负年份或 XML 架构集合中的默认值都将自动更新为基 **xs:date** 或 **xs:dateTime** 类型允许的最小值（例如，对于 **xs:dateTime**，则更新为 0001-01-01T00:00:00.0000000Z）。  
  
 请注意，即使 XML 数据类型包含负年份，仍可以使用简单的 SQL SELECT 语句来检索整个 XML 数据类型。 建议您用新的受支持范围内的年份替代负年份，或将相应元素或属性的类型更改为 **xs:string**。  
  
## <a name="see-also"></a>请参阅  
 [创建 XML 数据的实例](create-instances-of-xml-data.md)   
 [xml 数据类型方法](/sql/t-sql/xml/xml-data-type-methods)   
 [XML 数据修改语言 (XML DML)](/sql/t-sql/xml/xml-data-modification-language-xml-dml)   
 [XML 数据 (SQL Server)](xml-data-sql-server.md)  
  
  
