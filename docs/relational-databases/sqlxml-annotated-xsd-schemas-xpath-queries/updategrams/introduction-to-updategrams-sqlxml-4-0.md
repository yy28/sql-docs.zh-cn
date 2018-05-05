---
title: Updategram (SQLXML 4.0) 简介 |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6c3d51e64669f2410ca6e99926734b767dba1f45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Updategram 简介 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  你可以修改 （插入、 更新或删除） 中的数据库[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]从现有 XML 文档使用属的 updategram 或 OPENXML[!INCLUDE[tsql](../../../includes/tsql-md.md)]函数。  
  
 OPENXML 函数通过拆分现有 XML 文档并提供可以传递给 INSERT、UPDATE 或 DELETE 语句的行集来修改数据库。 使用 OPENXML 时，直接针对数据库表进行操作。 因此，在行集提供程序（如表）可以显示为源时，最适合使用 OPENXML。  
  
 与 OPENXML 一样，updategram 允许您在数据库中插入、更新或删除数据；不过，updategram 针对带批注的 XSD（或 XDR）架构提供的 XML 视图进行操作，例如将更新应用于映射架构提供的 XML 视图。 而映射架构则具有将 XML 元素和属性映射到相应的数据库表和列所需的信息。 updategram 使用此映射信息更新数据库表和列。  
  
> [!NOTE]  
>  本文档假定您熟悉 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的模板和映射架构支持。 有关详细信息，请参阅[简介批注 XSD 架构 & #40;SQLXML 4.0 & #41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). 有关使用 XDR 的旧版应用程序，请参阅[批注 XDR 架构&#40;SQLXML 4.0 中弃用&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="required-namespaces-in-the-updategram"></a>Updategram 中必需的命名空间  
 属的 updategram 中的关键字如**\<同步 >**， **\<之前 >**，和**\<后 >**，存在于**urn： 架构-microsoft-com:xml-属的 updategram**命名空间。 您可以为该命名空间使用任意前缀。 在本文档中， **updg**前缀表示**属的 updategram**命名空间。  
  
## <a name="reviewing-syntax"></a>查看语法  
 Updategram 是与模板**\<同步 >**， **\<之前 >**，和**\<后 >** 窗体的语法的块属的 updategram。 以下代码显示了此语法的最简单形式：  
  
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
  
 **\<before>**  
 标识记录实例的现有状态（也称为“以前状态”）。  
  
 **\<after>**  
 标识要将数据更改到的新状态。  
  
 **\<sync>**  
 包含**\<之前 >** 和**\<后 >** 块。 A **\<同步 >** 块可以包含多个组的**\<之前 >** 和**\<后 >** 块。 如果存在多个集的**\<之前 >** 和**\<后 >** 块，这些块 （即使它们是空的） 必须指定为对。 此外，属的 updategram 可以有多个**\<同步 >** 块。 每个**\<同步 >** 块是一个单位的事务 (这意味着，任一中的所有内容**\<同步 >** 完成块或不做任何操作)。 如果指定多个**\<同步 >** 属的 updategram，发生的故障中的块**\<同步 >** 块不会影响其他**\<同步>** 块。  
  
 Updategram 是否删除、 插入或更新的记录实例依赖于的内容**\<之前 >** 和**\<后 >** 块：  
  
-   如果仅在显示的记录实例**\<之前 >** 块中没有相应实例**\<后 >** 块，属的 updategram 执行删除操作。  
  
-   如果仅在显示的记录实例**\<后 >** 块中没有相应实例**\<之前 >** 块，此操作是插入操作。  
  
-   如果中显示的记录实例**\<之前 >** 阻止和都有相应的实例**\<后 >** 块，此操作是更新操作。 在这种情况下，属的 updategram 中指定的值更新的记录实例**\<后 >** 块。  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>在 Updategram 中指定映射架构  
 在 updategram 中，映射架构（支持 XSD 和 XDR 架构）所提供的 XML 抽象可以是隐式的，也可以是显式的（即无论是否指定映射架构，updategram 都可以工作）。 如果未指定的映射架构，属的 updategram 假定的隐式映射 （默认映射），其中在每个元素**\<之前 >** 块或**\<后 >** 块映射到表和每个元素的子元素或属性将映射到数据库中的列。 如果显式指定映射架构，updategram 中的元素和属性必须与映射架构中的元素和属性匹配。  
  
### <a name="implicit-default-mapping"></a>隐式（默认）映射  
 在大多数情况下，执行简单更新的 updategram 可能不需要映射架构。 此时 updategram 依赖于默认映射架构。  
  
 以下 updategram 演示隐式映射。 在此示例中，updategram 在 Sales.Customer 表中插入一个新客户。 因为此属的 updategram 使用隐式映射\<Sales.Customer > 元素映射到 Sales.Customer 表，并 CustomerID 和 SalesPersonID 属性将映射到 Sales.Customer 表中的相应列。  
  
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
  
 如果属的 updategram 执行复杂的更新 （例如，在基于映射架构中指定的父-子关系的多个表的插入记录） 时，必须通过使用显式提供映射架构**映射架构**针对其中属的 updategram 的执行属性。  
  
 由于 updategram 是模板，因此为 updategram 中的映射架构指定的路径是相对于模板文件的位置而言（即相对于存储 updategram 的位置而言）。 有关详细信息，请参阅[指定批注映射架构中属的 Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Updategram 中以元素为中心的映射和以属性为中心的映射  
 使用默认映射（在 updategram 中未指定映射架构）时，如果是以元素为中心的映射，则 updategram 元素映射到表并且子元素映射到列。如果是以属性为中心的映射，则属性映射到列。  
  
### <a name="element-centric-mapping"></a>以元素为中心的映射  
 在以元素为中心的 updategram 中，元素包含指示元素属性的子元素。 请参阅以下 updategram 示例。 **\<Person.Contact >** 元素包含 **\<FirstName >** 和 **\<LastName >** 子元素。 属性，这些子元素是 **\<Person.Contact >** 元素。  
  
 由于此属的 updategram 未指定的映射架构，属的 updategram 使用隐式映射，其中 **\<Person.Contact >** 元素映射到 Person.Contact 表并及其子元素将映射到 FirstName 和LastName 列。  
  
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
 在以属性为中心的映射中，元素具有属性。 以下 updategram 使用以属性为中心的映射。 在此示例中，  **\<Person.Contact >** 元素组成**FirstName**和**LastName**属性。 这些属性是的属性 **\<Person.Contact >** 元素。 与前面的示例中，此属的 updategram 指定没有映射架构中，，因此它依赖于要映射的隐式映射 **\<Person.Contact >** 到 Person.Contact 表和元素的特性移动到的元素表中的相应列。  
  
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
 可以组合使用以元素为中心的映射和以属性为中心的映射，如以下 updategram 中所示。 请注意，  **\<Person.Contact >** 元素包含属性和子元素。 此 updategram 也依赖于隐式映射。 因此， **FirstName**属性和 **\<LastName >** 子元素映射到 Person.Contact 表中相应列。  
  
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
  
 有效的字符进行编码[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]标识符但不是有效的 XML 标识符，请使用 __xHHHH\_\_作为编码的值，其中 HHHH 代表最中的字符的四位十六进制 ucs-2 代码重要的位优先顺序。 使用此编码方案，空格字符获取替换 x0020 （的四位十六进制代码空格字符）;因此，表中的名称 [订单详细信息][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]变得 _x005B_Order_x0020_Details_x005D\_在 XML 中。  
  
 同样，你可能需要指定由三部分元素名称，如\<[数据库]。 [所有者]。[表] >。 因为括号字符 （[和]） 无效的 XML 中，你必须指定为\<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_>，其中 _x005B\_是编码左的方括号 ([) 和 _x005D\_是右括号 (]) 的编码。  
  
## <a name="executing-updategrams"></a>执行 Updategram  
 由于 updategram 是模板，因此模板的所有处理机制均适用于 updategram。 对于 SQLXML 4.0，可以通过以下方式之一来执行 updategram：  
  
-   在 ADO 命令中提交它。  
  
-   将其作为 OLE DB 命令提交。  
  
## <a name="see-also"></a>另请参阅  
 [属的 Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
