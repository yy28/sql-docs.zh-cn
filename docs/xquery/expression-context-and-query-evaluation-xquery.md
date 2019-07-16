---
title: 表达式上下文和查询计算 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expression context [XQuery]
- XQuery, expression context
- XQuery, query evaluation
- static context
- dynamic context [XQuery]
ms.assetid: 5059f858-086a-40d4-811e-81fedaa18b06
author: rothja
ms.author: jroth
ms.openlocfilehash: d665b16c6b635da8b267ac0549ab8d918af8c06b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038919"
---
# <a name="expression-context-and-query-evaluation-xquery"></a>表达式上下文和查询计算 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  表达式的上下文是用于分析和计算表达式的信息。 下面是计算 XQuery 的两个阶段：  
  
-   **静态上下文**-这是查询编译阶段。 根据可用信息，有时会在对查询进行静态分析过程中产生错误。  
  
-   **动态上下文**-这是查询执行阶段。 即使查询没有静态错误（如在查询编译过程中产生的错误），查询也可能在执行过程中返回错误。  
  
## <a name="static-context"></a>静态上下文  
 静态上下文初始化指的是将有关对表达式进行的静态分析的所有信息放在一起的过程。 在静态上下文初始化中，要完成下列内容：  
  
-   **的边界空格**策略设置为 strip。 因此，由不保留边界空格**任何元素**并**属性**查询中的构造函数。 例如：  
  
    ```  
    declare @x xml  
    set @x=''  
    select @x.query('<a>  {"Hello"}  </a>,  
  
        <b> {"Hello2"}  </b>')  
    ```  
  
     此查询返回以下结果，得到这种结果是因为在分析 XQuery 表达式过程中删除了边界空格：  
  
    ```  
    <a>Hello</a><b>Hello2</b>  
    ```  
  
-   为下列内容初始化前缀和命名空间绑定：  
  
    -   一组预定义的命名空间。  
  
    -   使用 WITH XMLNAMESPACES 定义的所有命名空间。 有关详细信息，请参阅[命名空间添加到查询使用 WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md))。  
  
    -   查询 Prolog 中定义的所有命名空间。 请注意，Prolog 中的命名空间声明可覆盖 WITH XMLNAMESPACES 中的命名空间声明。 例如，在以下查询中，WITH XMLNAMESPACES 声明将其绑定到命名空间的前缀 (pd) (`https://someURI`)。 但是，在 WHERE 子句中，查询 Prolog 覆盖该绑定。  
  
        ```  
        WITH XMLNAMESPACES ('https://someURI' AS pd)  
        SELECT ProductModelID, CatalogDescription.query('  
            <Product   
                ProductModelID= "{ sql:column("ProductModelID") }"   
                />  
        ') AS Result  
        FROM Production.ProductModel  
        WHERE CatalogDescription.exist('  
            declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             /pd:ProductDescription[(pd:Specifications)]'  
            ) = 1  
        ```  
  
     所有这些命名空间绑定都在静态上下文初始化过程中解析。  
  
-   如果查询类型化**xml**列或变量，将导入到静态上下文与列或变量相关联的 XML 架构集合的组件。 有关详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
-   对于导入架构中的每个原子类型，也可在静态上下文中使用转换函数。 下面的示例说明了这一点。 在此示例中，指定一个查询针对类型化**xml**变量。 与此变量关联的 XML 架构集合定义了原子类型 myType。 此类型的转换函数相对应**myType()** ，可在静态分析过程。 查询表达式 (`ns:myType(0)`) 返回 myType 类型的值。  
  
    ```  
    -- DROP XML SCHEMA COLLECTION SC  
    -- go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <simpleType name="myType">  
                <restriction base="int">  
                 <enumeration value="0" />  
                  <enumeration value="1"/>  
                </restriction>  
          </simpleType>  
          <element name="root" type="ns:myType"/>  
    </schema>'  
    go  
  
    DECLARE @var XML(SC)  
    SET @var = '<root xmlns="myNS">0</root>'  
    -- specify myType() casting function in the query  
    SELECT @var.query('declare namespace ns="myNS"; ns:myType(0)')  
    ```  
  
     在下面的示例中，为强制转换函数**int**在表达式中指定内置 XML 类型。  
  
    ```  
    declare @x xml  
    set @x = ''  
    select @x.query('xs:int(5)')  
    go  
    ```  
  
 初始化静态上下文后，将分析（编译）查询表达式。 静态分析涉及以下内容：  
  
1.  查询分析。  
  
2.  解析在表达式中指定的函数和类型名称。  
  
3.  对查询执行静态类型化。 这可确保查询类型安全。 例如，以下查询返回静态错误，因为 **+** 运算符要求 numeric primitive 类型参数：  
  
    ```  
    declare @x xml  
    set @x=''  
    SELECT @x.query('"x" + 4')  
    ```  
  
     在以下示例中， **value （)** 运算符要求单一参数。 根据指定的 XML 架构中，可以有多个\<Elem > 元素。 对表达式进行的静态分析确定它是非类型安全，并返回静态错误。 若要解决该错误，必须重写表达式以显式指定单一参数 (`data(/x:Elem)[1]`)。  
  
    ```  
    DROP XML SCHEMA COLLECTION SC  
    go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <element name="Elem" type="string"/>  
    </schema>'  
    go  
  
    declare @x xml (SC)  
    set @x='<Elem xmlns="myNS">test</Elem><Elem xmlns="myNS">test2</Elem>'  
    SELECT @x.value('declare namespace x="myNS"; data(/x:Elem)[1]','varchar(20)')  
    ```  
  
     有关详细信息，请参阅[XQuery 与静态类型化](../xquery/xquery-and-static-typing.md)。  
  
### <a name="implementation-restrictions"></a>实现限制  
 下面是与静态上下文有关的限制：  
  
-   不支持 XPath 兼容模式。  
  
-   对于 XML 构造，仅支持 strip 构造模式。 这是默认设置。 因此，构造的元素节点的类型为**xdt： 非类型化**类型，并且属性属于**xdt: untypedatomic**类型。  
  
-   仅支持 ordered 排序模式。  
  
-   仅支持 strip XML 空格策略。  
  
-   不支持基准 URI 功能。  
  
-   **fn:doc()** 不受支持。  
  
-   **fn:collection()** 不受支持。  
  
-   不提供 XQuery 静态标记。  
  
-   与关联的排序规则**xml**使用数据类型。 将此排序规则始终设置为 Unicode 码位排序规则。  
  
## <a name="dynamic-context"></a>动态上下文  
 动态上下文指的是在执行表达式时必须可用的信息。 除了静态上下文以外，在动态上下文初始化中，还要完成下列内容：  
  
-   初始化上下文项、上下文位置和上下文大小等表达式的主要项，如下所示。 请注意，所有这些值可以通过重写[nodes （） 方法](../t-sql/xml/nodes-method-xml-data-type.md)。  
  
    -   **Xml**数据类型设置的上下文项，为文档节点正在处理的节点。  
  
    -   上下文位置（即上下文项相对于正在处理的节点的位置）首先设置为 1。  
  
    -   上下文大小（正在处理的序列中的项数）首先设置为 1，因为始终有一个文档节点。  
  
### <a name="implementation-restrictions"></a>实现限制  
 下面是与动态上下文有关的限制：  
  
-   **当前日期和时间**上下文函数**fn:current-日期**， **fn:current-时间**，以及**fn:current-dateTime**，不是受支持。  
  
-   **隐式时区**固定为 UTC + 0，不能更改。  
  
-   **Fn:doc()** 不支持函数。 所有查询都执行针对**xml**类型列或变量。  
  
-   **Fn:collection()** 不支持函数。  
  
## <a name="see-also"></a>请参阅  
 [XQuery 基础知识](../xquery/xquery-basics.md)   
 [类型化的 XML 与非类型化的 XML 的比较](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 架构集合 (SQL Server)](../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
