---
title: "将 EXPLICIT 模式与 FOR XML 一起使用 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EXPLICIT FOR XML mode
- FOR XML clause, EXPLICIT mode
- FOR XML EXPLICIT mode
ms.assetid: 8b26e8ce-5465-4e7a-b237-98d0f4578ab1
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9d8bace5c696e49a9bfe92664a80030d867ae237
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="use-explicit-mode-with-for-xml"></a>将 EXPLICIT 模式与 FOR XML 一起使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]如主题[使用 FOR XML 构造 XML](../../relational-databases/xml/for-xml-sql-server.md) 中所述，使用 RAW 和 AUTO 模式不能很好地控制从查询结果生成的 XML 的形状。 但是，对于要从查询结果生成 XML，EXPLICIT 模式会提供非常好的灵活性。  
  
 必须以特定的方式编写 EXPLICIT 模式查询，以便将有关所需的 XML 的附加信息（如 XML 中的所需嵌套）显式指定为查询的一部分。 根据所请求的 XML，编写 EXPLICIT 模式查询可能会很烦琐。 您会发现 [使用 PATH 模式](../../relational-databases/xml/use-path-mode-with-for-xml.md) （具有嵌套）相对编写 EXPLICIT 模式查询而言更加简单。  
  
 因为将所需的 XML 描述为 EXPLICIT 模式查询的一部分，所以必须确保生成的 XML 格式正确且有效。  
  
## <a name="rowset-processing-in-explicit-mode"></a>EXPLICIT 模式下的行集处理  
 EXPLICIT 模式会将由查询执行生成的行集转换为 XML 文档。 为使 EXPLICIT 模式生成 XML 文档，行集必须具有特定的格式。 这需要您编写 SELECT 查询以生成具有特定格式的行集（通用表 ），以便处理逻辑随后可以生成所需的 XML。  
  
 首先，查询必须生成下列两个元数据列：  
  
-   第一列必须提供当前元素的标记号（整数类型），并且列名必须是 **Tag**。 查询必须为从行集构造的每个元素提供唯一标记号。  
  
-   第二列必须提供父元素的标记号，并且此列的列名必须是 **Parent**。 这样，Tag 和 Parent 列将提供层次结构信息。  
  
 这些元数据列值与列名中的信息一起都用于生成所需的 XML。 请注意，查询必须以特定的方式提供列名。 同时请注意， **Parent** 列中的 0 或 NULL 表明相应的元素没有父级。 该元素将作为顶级元素添加到 XML。  
  
 为了了解如何将查询生成的通用表处理为生成 XML 结果，假定您已经编写了一个生成此通用表的查询：  
  
 ![通用表示例](../../relational-databases/xml/media/xmlutable.gif "通用表示例")  
  
 注意有关此通用表的以下事项：  
  
-   前两列是 **Tag** 和 **Parent** ，它们是元数据列。 这些值确定层次结构。  
  
-   列名是以特定的方式指定的，本主题的后面部分将进行介绍。  
  
-   从此通用表生成 XML 的过程中，此表中的数据被垂直分区到列组中。 分组是根据 **Tag** 值和列名确定的。 在构造 XML 的过程中，处理逻辑为每行选择一组列，然后构造一个元素。 在此示例中，将应用以下规则：  
  
    -   对于第一行中的 **Tag** 列值 1，名称中包括此相同标记号的列（**Customer!1!cid** 和 **Customer!1!name**）形成一组。 这些列用于处理行，您可能已经注意到所生成元素的形式为 <`Customer id=... name=...`>。 列名格式在本主题的后面部分进行介绍。  
  
    -   对于 **Tag** 列值为 2 的行，列 **Order!2!id** 和 **Order!2!date** 形成一组，然后该组用于构造元素（形式为 <`Order id=... date=... /`>）。  
  
    -   对于 **Tag** 列值为 3 的行，列 **OrderDetail!3!id!id** 和 **OrderDetail!3!pid!idref** 形成一组。 其中每一行都从这些列生成一个元素（形式为 <`OrderDetail id=... pid=...`>）。  
  
-   请注意，在生成 XML 层次结构的过程中，行是按顺序处理的。 XML 层次结构确定如下：  
  
    -   第一行指定 **Tag** 值为 1， **Parent** 值为 NULL。 因此，相应的元素（即 <`Customer`> 元素）将作为顶级元素添加在 XML 中。  
  
        ```  
        <Customer cid="C1" name="Janine">  
        ```  
  
    -   第二行指定 **Tag** 值为 2， **Parent** 值为 1。 因此，将添加 <`Order`> 元素作为 <`Customer`> 元素的子元素。  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
        ```  
  
    -   接下来的两行指定 **Tag** 值为 3， **Parent** 值为 2。 因此，将添加两个 <`OrderDetail`> 元素作为 <`Order`> 元素的子元素。  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
        ```  
  
    -   最后一行确定 **Tag** 号为 2， **Parent** 标记号为 1。 因此，另一个 <`Order`> 元素将作为 <`Customer`> 父元素的子元素添加。  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
           </Order>  
           <Order id="O2" date="3/29/1997">  
        </Customer>  
        ```  
  
 简言之，使用 EXPLICIT 模式时， **Tag** 和 **Parent** 元数据列中的值、列名中提供的信息以及正确的行顺序将生成所需的 XML。  
  
### <a name="universal-table-row-ordering"></a>通用表行顺序  
 在构造 XML 过程中，通用表中的行是按顺序处理的。 因此，若要检索到与其父级关联的正确的子级实例，必须对行集中的行进行排序，以便每个父节点后紧跟着其子节点。  
  
## <a name="specifying-column-names-in-a-universal-table"></a>指定通用表中的列名  
 在编写 EXPLICIT 模式查询时，必须使用以下格式指定所得到的行集中的列名。 它们提供转换信息（包括元素名称和属性名称）以及用指令指定的其他附加信息。  
  
 常用格式如下：  
  
```  
  
ElementName!TagNumber!AttributeName!Directive  
```  
  
 下面是对格式各部分的说明。  
  
 *ElementName*  
 是所生成元素的通用标识符。 例如，如果将 **Customers** 指定为 *ElementName*，将生成 \<Customers> 元素。  
  
 *TagNumber*  
 是分配给元素的唯一标记值。 在两个元数据列（ **Tag** 和 **Parent**）的帮助下，此值将确定所得到的 XML 中的元素的嵌套。  
  
 *AttributeName*  
 提供要在指定的 *ElementName*中构造的属性的名称。 如果没有指定 *Directive* ，将发生这种行为。  
  
 如果指定了 *Directive* 并且它是 **xml**、 **cdata**或 **element**，则此值用于构造 *ElementName*的子元素，并且此列值将添加到该子元素。  
  
 如果指定了 *Directive*，则 *AttributeName* 可以为空。 例如 ElementName!TagNumber!!Directive。 在这种情况下，列值直接由 *ElementName*包含。  
  
 *Directive*  
 *Directive* 是可选的，可以使用它来提供有关 XML 构造的其他信息。 *Directive* 有两种用途。  
  
 一种用途是将值编码为 ID、IDREF 和 IDREFS。 可以将 **ID**、 **IDREF**和 **IDREFS** 关键字指定为 *Directives*。 这些指令将覆盖属性类型。 这使您能够创建文档内链接。  
  
 同时，可以使用 *Directive* 来指示如何将字符串数据映射到 XML。 可以将 **hide**、 **element、elementxsinil**、 **xml**、 **xmltext**和 **cdata** 关键字用作 *Directive*。 **hide** 指令会隐藏节点。 当仅为排序目的而检索值，但又不想让它们出现在所得到的 XML 中时，此指令非常有用。  
  
 **element** 指令生成的结果中包含元素而不是属性。 包含的数据被编码为实体。 例如， **<** 字符变成 &lt;。 对于 NULL 列值，不会生成任何元素。 如果要为 NULL 列值生成元素，可以指定 **elementxsinil** 指令。 这将生成具有属性 xsi:nil=TRUE 的元素。  
  
 除不发生实体编码外， **xml** 指令与 **element** 指令相同。 请注意，可以将 **element** 指令与 **ID**、 **IDREF**或 **IDREFS**结合使用，然而不允许 **xml** 指令与除 **hide**指令之外的任何其他指令结合使用。  
  
 **cdata** 指令通过将数据与 CDATA 部分包装在一起来包含数据。 不对内容进行实体编码。 原始数据类型必须是文本类型（如 **varchar**、 **nvarchar**、 **text**或 **ntext**）。 此指令只适用于 **hide**。 当使用此指令时，不能指定 *AttributeName* 。  
  
 大多数情况下，允许在这两个组之间组合指令，但不允许在它们自身当中组合指令。  
  
 如果未指定 *Directive* 和 *AttributeName* （例如 **Customer!1**），则暗含一个 **element** 指令（如 **Customer!1!!element**），并且列数据包含在 *ElementName*中。  
  
 如果指定了 **xmltext** 指令，则列内容包装在与文档的其余部分集成在一起的单个标记中。 在提取由 OPENXML 存储在列中的溢出（未用完的）XML 数据时，此指令很有用。 有关详细信息，请参阅 [OPENXML (SQL Server)](../../relational-databases/xml/openxml-sql-server.md)。  
  
 如果指定了 *AttributeName* ，将由指定的名称替换标记名。 否则，将通过把内容置于包容的起始位置（不经过实体编码）将属性追加到闭合元素属性的当前列表中。 包含此指令的列必须是文本类型（如 **varchar**、 **nvarchar**、 **char**、 **nchar**、 **text**或 **ntext**）。 此指令只适用于 **hide**。 在提取列中存储的溢出数据时，此指令很有用。 如果内容的 XML 格式不正确，则未定义该行为。  
  
## <a name="in-this-section"></a>本节内容  
 下列示例说明了 EXPLICIT 模式的用法。  
  
-   [示例：检索雇员信息](../../relational-databases/xml/example-retrieving-employee-information.md)  
  
-   [示例：指定 ELEMENT 指令](../../relational-databases/xml/example-specifying-the-element-directive.md)  
  
-   [示例：指定 ELEMENTXSINIL 指令](../../relational-databases/xml/example-specifying-the-elementxsinil-directive.md)  
  
-   [示例：使用 EXPLICIT 模式构造同级](../../relational-databases/xml/example-constructing-siblings-with-explicit-mode.md)  
  
-   [示例：指定 ID 和 IDREF 指令](../../relational-databases/xml/example-specifying-the-id-and-idref-directives.md)  
  
-   [示例：指定 ID 和 IDREFS 指令](../../relational-databases/xml/example-specifying-the-id-and-idrefs-directives.md)  
  
-   [示例：指定 HIDE 指令](../../relational-databases/xml/example-specifying-the-hide-directive.md)  
  
-   [示例：指定 ELEMENT 指令和实体编码](../../relational-databases/xml/example-specifying-the-element-directive-and-entity-encoding.md)  
  
-   [示例：指定 CDATA 指令](../../relational-databases/xml/example-specifying-the-cdata-directive.md)  
  
-   [示例：指定 XMLTEXT 指令](../../relational-databases/xml/example-specifying-the-xmltext-directive.md)  
  
## <a name="see-also"></a>另请参阅  
 [将 RAW 模式与 FOR XML 一起使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)   
 [将 AUTO 模式与 FOR XML 一起使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [将 PATH 模式与 FOR XML 一起使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
