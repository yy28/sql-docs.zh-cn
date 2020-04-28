---
title: Updategram 简介（SQLXML）
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- updategrams [SQLXML], mapping schema specifying
- namespaces [SQLXML]
- updategrams [SQLXML], about updategrams
- attribute-centric mapping
- invalid characters [SQLXML]
- element-centric mapping [SQLXML]
- mapping schema [SQLXML], updategrams
- namespaces [SQLXML], updategrams
- executing updategrams [SQLXML]
- implicit schema mapping
ms.assetid: cfe24e82-a645-4f93-ab16-39c21f90cce6
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c9e709a607d02273c0e2cb0208faf4e9799acf6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "75252479"
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Updategram 简介 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  通过使用 updategram 或 OPENXML [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)]函数，可以从现有的 XML 文档中修改（插入、更新或删除）数据库。  
  
 OPENXML 函数通过拆分现有 XML 文档并提供可以传递给 INSERT、UPDATE 或 DELETE 语句的行集来修改数据库。 使用 OPENXML 时，直接针对数据库表进行操作。 因此，在行集提供程序（如表）可以显示为源时，最适合使用 OPENXML。  
  
 与 OPENXML 一样，updategram 允许您在数据库中插入、更新或删除数据；不过，updategram 针对带批注的 XSD（或 XDR）架构提供的 XML 视图进行操作，例如将更新应用于映射架构提供的 XML 视图。 而映射架构则具有将 XML 元素和属性映射到相应的数据库表和列所需的信息。 updategram 使用此映射信息更新数据库表和列。  
  
> [!NOTE]  
>  本文档假定您熟悉 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的模板和映射架构支持。 有关详细信息，请参阅[&#40;SQLXML 4.0&#41;中带批注的 XSD 架构简介](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)。 对于使用 XDR 的旧版应用程序，请参阅[SQLXML 4.0&#41;中 &#40;弃用的带批注 XDR 架构](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="required-namespaces-in-the-updategram"></a>Updategram 中必需的命名空间  
 Updategram 中的关键字（如** \<同步>**、 ** \<>之前**和** \<>之后**）存在于**urn：架构-microsoft com： updategram**命名空间中。 您可以为该命名空间使用任意前缀。 在本文档中， **updg**前缀表示**updategram**命名空间。  
  
## <a name="reviewing-syntax"></a>检查语法  
 Updategram 是一个模板，其中包含** \<同步>**、 ** \<>之前**以及** \<** 形成 updategram 语法>块之后。 以下代码显示了此语法的最简单形式：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema= "AnnotatedSchemaFile.xml"] >  
    <updg:before>  
        ...  
    </updg:before>  
    <updg:after>  
        ...  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 以下定义描述了其中每个块的作用：  
  
 **\<>之前**  
 标识记录实例的现有状态（也称为“以前状态”）。  
  
 **\<之后>**  
 标识要将数据更改到的新状态。  
  
 **\<同步>**  
 包含** \<>之前**和** \<之后>** 块。 同步>块可以包含>块** \<之前>** 和** \<后面**的多个集。 ** \<** 如果** \<在>之前**和** \<>块之后**有多个集，则这些块（即使它们为空）必须指定为成对。 此外，updategram 可以有多个** \<sync>** 块。 每个** \<同步>** 块都是一个事务单元（这意味着** \<同步>** 块中的所有内容均已完成或未执行任何操作）。 如果在 updategram 中指定多个** \<同步>** 块，则一个** \<同步>** 块的失败不会影响其他** \<同步>** 块。  
  
 Updategram 是删除、插入还是更新记录实例取决于** \<>之前**和** \<>块后**的内容：  
  
-   如果记录实例只出现在** \<>** 块中没有对应实例的** \<之前>** 块中，则 updategram 将执行删除操作。  
  
-   如果记录实例只出现在** \<之前** ** \<>** 块中，而在>块中没有对应的实例，则这是一个插入操作。  
  
-   如果记录实例出现在>块** \<之前**，且在** \<>** 块中具有相应的实例，则它是更新操作。 在这种情况下，updategram 会将记录实例更新为** \<>块后**指定的值。  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>在 Updategram 中指定映射架构  
 在 updategram 中，映射架构（支持 XSD 和 XDR 架构）所提供的 XML 抽象可以是隐式的，也可以是显式的（即无论是否指定映射架构，updategram 都可以工作）。 如果未指定映射架构，则 updategram 将采用隐式映射（默认映射），其中** \<>** 块中** \<>** 的每个元素映射到表，每个元素的子元素或属性映射到数据库中的列。 如果显式指定映射架构，updategram 中的元素和属性必须与映射架构中的元素和属性匹配。  
  
### <a name="implicit-default-mapping"></a>隐式（默认）映射  
 在大多数情况下，执行简单更新的 updategram 可能不需要映射架构。 此时 updategram 依赖于默认映射架构。  
  
 以下 updategram 演示隐式映射。 在此示例中，updategram 在 Sales.Customer 表中插入一个新客户。 因为此 updategram 使用隐式映射， \<所以 customer> 元素映射到 customer 表，CustomerID 和 SalesPersonID 属性映射到 customer 表中的相应列。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
</updg:before>  
<updg:after>  
    <Sales.Customer CustomerID="1" SalesPersonID="277" />  
    </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="explicit-mapping"></a>显式映射  
 如果指定映射架构（XSD 或 XDR），则 updategram 使用该架构确定要更新的数据库表和列。  
  
 如果 updategram 执行复杂更新（例如，基于映射架构中指定的父子关系在多个表中插入记录），则必须通过使用 updategram 执行的**映射架构**特性来显式提供映射架构。  
  
 由于 updategram 是模板，因此为 updategram 中的映射架构指定的路径是相对于模板文件的位置而言（即相对于存储 updategram 的位置而言）。 有关详细信息，请参阅[在 Updategram 中指定带批注的映射架构 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Updategram 中以元素为中心的映射和以属性为中心的映射  
 使用默认映射（在 updategram 中未指定映射架构）时，如果是以元素为中心的映射，则 updategram 元素映射到表并且子元素映射到列。如果是以属性为中心的映射，则属性映射到列。  
  
### <a name="element-centric-mapping"></a>以元素为中心的映射  
 在以元素为中心的 updategram 中，元素包含指示元素属性的子元素。 请参阅以下 updategram 示例。 Person>元素包含** \<FirstName>** 和** \<LastName>** 子元素。 ** \<** 这些子元素是** \<用户的属性。请联系>** 元素。  
  
 由于此 updategram 未指定映射架构，因此 updategram 将使用隐式映射，其中** \<person>** 元素映射到 person 表，并将其子元素映射到 FirstName 和 LastName 列。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:after>  
    <Person.Contact>  
       <FirstName>Catherine</FirstName>  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="attribute-centric-mapping"></a>以属性为中心的映射  
 在以属性为中心的映射中，元素具有属性。 以下 updategram 使用以属性为中心的映射。 在此示例中， ** \<Person>** 元素包含**FirstName**和**LastName**属性。 这些属性是** \<用户的属性。请联系>** 元素。 如前面的示例所示，此 updategram 不指定任何映射架构，因此它依赖于隐式映射来映射** \<person。>请联系**表中的相应列，并将元素的属性与表中的相应列联系在一起。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" LastName="Abel" />  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="using-both-element-centric-and-attribute-centric-mapping"></a>同时使用以元素为中心的映射和以属性为中心的映射  
 可以组合使用以元素为中心的映射和以属性为中心的映射，如以下 updategram 中所示。 请注意， ** \<Person>** 元素包含特性和子元素。 此 updategram 也依赖于隐式映射。 因此， **FirstName**属性和** \<LastName>** 子元素映射到 Person 表中的相应列。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" >  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="working-with-characters-valid-in-sql-server-but-not-valid-in-xml"></a>使用在 SQL Server 中有效但在 XML 中无效的字符  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，表名称可以包含空格。 但是，此类表名称在 XML 中无效。  
  
 若要对是有效[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]标识符，但不是有效 XML 标识符的字符进行编码\_\_，请使用 "__xHHHH" 作为编码值，其中 HHHH 代表最高有效位第一次的字符的四位十六进制 UCS-2 代码。 使用此编码方案时，空格字符将替换为 x0020 （空格字符的四位十六进制代码）;因此，中的表名 [Order Details] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]在 XML\_中变为 _x005B_Order_x0020_Details_x005D。  
  
 同样，你可能需要指定由三个部分组成的元素名称， \<如 [database]。[owner]。[表] >。 由于方括号字符（[和]）在 XML 中无效，因此您必须将其指定为\<_x005B_database_x005D\__x005B_owner_x005D\__x005B_table_x005D\_>，其中 _x005B\_是左括号（[）的编码，_x005D\_是右括号（]）的编码。  
  
## <a name="executing-updategrams"></a>执行 Updategram  
 由于 updategram 是模板，因此模板的所有处理机制均适用于 updategram。 对于 SQLXML 4.0，可以通过以下方式之一来执行 updategram：  
  
-   在 ADO 命令中提交它。  
  
-   将其作为 OLE DB 命令提交。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全注意事项](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
