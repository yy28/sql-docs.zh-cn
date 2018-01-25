---
title: "FOR 子句 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FOR
- FOR CLAUSE
- FOR_TSQL
- FOR_CLAUSE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- XML option [SQL Server]
- BROWSE option
- FOR clause [Transact-SQL]
ms.assetid: 08a6f084-8f73-4f2a-bae4-3c7513dc99b9
caps.latest.revision: "54"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 085a9c7f6422c70cc43086d2174a5c7aa485040e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="select---for-clause-transact-sql"></a>SELECT-FOR 子句 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  FOR 子句用于指定查询结果的以下选项之一。  
  
-   允许在浏览模式游标中查看查询结果，通过指定的更新**FOR BROWSE**。  
  
-   通过指定查询结果作为 XML 的格式**FOR XML**。  
  
-   通过指定的格式查询结果设置为 JSON **FOR JSON**。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
[ FOR { BROWSE | <XML> | <JSON>} ]  
  
<XML> ::=  
XML   
{   
    { RAW [ ( 'ElementName' ) ] | AUTO }   
    [   
        <CommonDirectivesForXML>   
        [ , { XMLDATA | XMLSCHEMA [ ( 'TargetNameSpaceURI' ) ] } ]   
        [ , ELEMENTS [ XSINIL | ABSENT ]   
    ]  
  | EXPLICIT   
    [   
        <CommonDirectivesForXML>   
        [ , XMLDATA ]   
    ]  
  | PATH [ ( 'ElementName' ) ]   
    [  
        <CommonDirectivesForXML>   
        [ , ELEMENTS [ XSINIL | ABSENT ] ]  
    ]  
}   
  
<CommonDirectivesForXML> ::=   
[ , BINARY BASE64 ]  
[ , TYPE ]  
[ , ROOT [ ( 'RootName' ) ] ]  
  
<JSON> ::=  
JSON   
{   
    { AUTO | PATH }   
    [   
        [ , ROOT [ ( 'RootName' ) ] ]  
        [ , INCLUDE_NULL_VALUES ]  
        [ , WITHOUT_ARRAY_WRAPPER ]  
    ]  
  
}  
```  
  
## <a name="for-browse"></a>FOR BROWSE  
 BROWSE  
 指定可以在查看 DB-Library 浏览模式游标中的数据时进行更新。 表可以浏览应用程序中，如果表包括**时间戳**列，表具有一个唯一索引，并且 FOR BROWSE 选项是在发送到的实例的选择语句末尾[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  不能使用\<lock_hint > HOLDLOCK 中包括的 FOR BROWSE 选项的 SELECT 语句。
  
 FOR BROWSE 不能出现在由 UNION 运算符所联接的 SELECT 语句中。  
  
> [!NOTE]  
>  如果表的唯一索引键列可为空，并且表在外部联接的内侧，则浏览模式不支持索引。  
  
 使用浏览模式可以扫描 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中的行并逐行更新表中的数据。 访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表在浏览模式中的应用程序，你必须使用以下两个选项之一：  
  
-   用于访问中的数据的 SELECT 语句你[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表必须以关键字结束**FOR BROWSE**。 当你打开**FOR BROWSE**选项以使用浏览模式，将创建临时表。  
  
-   你必须运行以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句以使用启用浏览模式**NO_BROWSETABLE**选项：  
  
    ```  
    SET NO_BROWSETABLE ON  
    ```  
  
     当你打开**NO_BROWSETABLE**选项，所有 SELECT 语句的行为就像**FOR BROWSE**选项追加到语句。 但是， **NO_BROWSETABLE**选项不会创建临时表， **FOR BROWSE**选项通常用于将结果发送给你的应用程序。  
  
 当你尝试访问从数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的表使用 SELECT 查询，其中涉及到的外部联接语句，浏览模式，然后浏览模式时的外部联接语句内侧存在的表上定义唯一索引，不会不 sup端口的唯一索引。 仅当所有唯一索引键列可接受 Null 值时，浏览模式才支持唯一索引。 如果满足下列条件，浏览模式不支持唯一索引：  
  
-   你尝试访问中的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的表浏览模式通过 SELECT 查询，其中涉及到的外部联接语句。  
  
-   对外部联接语句内侧已存在的表定义唯一索引。  
  
 若要在浏览模式下重现此行为，请按下列步骤操作：  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，创建一个名为 SampleDB 的数据库。  
  
2.  在 SampleDB 数据库中，创建均包含名为 c1 的列的 tleft 表和 tright 表。 对 tleft 表中的 c1 列定义唯一索引，并将此列设置为接受 Null 值。 为此，请在相应的查询窗口中运行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
    ```  
    CREATE TABLE tleft(c1 INT NULL UNIQUE) ;  
    GO   
    CREATE TABLE tright(c1 INT NULL) ;  
    GO  
    ```  
  
3.  在 tleft 表和 tright 表中插入多个值。 请确保在 tleft 表中插入一个 Null 值。 为此，请在查询窗口中运行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
    ```  
    INSERT INTO tleft VALUES(2) ;  
    INSERT INTO tleft VALUES(NULL) ;  
    INSERT INTO tright VALUES(1) ;  
    INSERT INTO tright VALUES(3) ;  
    INSERT INTO tright VALUES(NULL) ;  
    GO  
    ```  
  
4.  开启**NO_BROWSETABLE**选项。 为此，请在查询窗口中运行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
    ```  
    SET NO_BROWSETABLE ON ;  
    GO  
    ```  
  
5.  通过在 SELECT 查询中使用外部联接语句来访问 tleft 表和 tright 表中的数据。 请确保 tleft 表位于外部联接语句的内侧。 为此，请在查询窗口中运行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
    ```  
    SELECT tleft.c1   
    FROM tleft   
    RIGHT JOIN tright   
    ON tleft.c1 = tright.c1   
    WHERE tright.c1 <> 2 ;  
  
    ```  
  
     请注意“结果”窗格中的以下输出：  
  
     c1  
  
     ---\-  
  
     NULL  
  
     NULL  
  
 在运行 SELECT 查询以便以浏览模式访问表之后，对于 tleft 表中的 c1 列，SELECT 查询的结果集包含两个 Null 值，这是因为在右外部联接语句中定义了该列。 因此，您无法在结果集中区分源自该表的 Null 值和右外部联接语句引入的 Null 值。 如果必须忽略结果集的 Null 值，则可能收到错误结果。  
  
> [!NOTE]  
>  如果唯一索引中包含的列不接受 Null 值，则结果集中的所有 Null 值都是由右外部联接语句引入的。  
  
## <a name="for-xml"></a>FOR XML  
 XML  
 指定以 XML 文档返回查询的结果。 必须指定下列 XML 模式之一：RAW、AUTO、EXPLICIT。 有关 XML 数据的详细信息和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[FOR XML &#40;SQL server&#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
 原始 [ **(***ElementName***)** ]  
 采用查询结果并将转换结果集合并到一个泛型标识符的 XML 元素中的每一行\<行 / > 作为元素标记。 （可选）可以为该行元素指定名称。 使用指定的生成的 XML 输出*ElementName*作为每行生成的行元素。 有关详细信息，请参阅[将 RAW 模式与 FOR XML 一起](../../relational-databases/xml/use-raw-mode-with-for-xml.md)和[将 RAW 模式与 FOR XML 一起](../../relational-databases/xml/use-raw-mode-with-for-xml.md)。  
  
 AUTO  
 以简单的嵌套 XML 树返回查询结果。 FROM 子句中每个在 SELECT 子句中至少列出一次的表都被表示为一个 XML 元素。 SELECT 子句中列出的列映射到适当的元素属性。 有关详细信息，请参阅 [将 AUTO 模式与 FOR XML 一起使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)。  
  
 EXPLICIT  
 指定显式定义产生的 XML 树的形状。 使用该模式要求必须以一种特定的方式编写查询，即显式指定与想要的嵌套有关的其他信息。 有关详细信息，请参阅 [将 EXPLICIT 模式与 FOR XML 一起使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)。  
  
 XMLDATA  
 返回内联 XDR 架构，但不将根元素添加到结果中。 如果指定了 XMLDATA，则 XDR 架构将被追加到文档末尾。  
  
> [!IMPORTANT]  
>  不推荐使用 XMLDATA 指令。 如果是 RAW 和 AUTO 模式，请使用 XSD 生成。 在 EXPLICIT 模式下，没有 XMLDATA 指令的替代项。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 XMLSCHEMA [ **('***TargetNameSpaceURI***')** ]  
 返回内联 XSD 架构。 如果指定该指令（用于返回架构中指定的命名空间），则可以选择指定目标命名空间 URI。 有关详细信息，请参阅 [生成内联 XSD 架构](../../relational-databases/xml/generate-an-inline-xsd-schema.md)。  
  
 ELEMENTS  
 指定列作为子元素返回。 否则，列将映射到 XML 属性。 只在 RAW、AUTO 和 PATH 模式中支持该选项。 有关详细信息，请参阅 [将 RAW 模式与 FOR XML 一起使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)。  
  
 XSINIL  
 指定具有的元素**xsi: nil**属性设置为**True**为 NULL 列值创建。 该选项只能与 ELEMENTS 指令一起指定。 有关详细信息，请参阅[使用 XSINIL 参数的 NULL 值生成元素](../../relational-databases/xml/generate-elements-for-null-values-with-the-xsinil-parameter.md)。  
  
 ABSENT  
 指示对于空列值，将不在 XML 结果中添加对应的 XML 元素。 该选项只能与 ELEMENTS 一起指定。  
  
 路径 [ **(***ElementName***)** ]  
 生成\<行 > 元素包装器结果集中的每一行。 你可以选择指定的元素名称\<行 > 元素包装。 如果提供空字符串，如 FOR XML PATH (**'**))，则不会生成包装元素。 使用 PATH 可能为使用 EXPLICIT 指令所编写的查询提供更简单的代替方案。 有关详细信息，请参阅 [将 PATH 模式与 FOR XML 一起使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)。  
  
 BINARY BASE64  
 指定查询返回二进制 base64 编码格式的二进制数据。 使用 RAW 和 EXPLICIT 模式检索二进制数据时，必须指定该选项。 这是 AUTO 模式中的默认值。  
  
 TYPE  
 指定查询返回的结果与**xml**类型。 有关详细信息，请参阅 [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md)。  
  
 ROOT [ **('***RootName***')** ]  
 指定将一个顶级元素添加到结果 XML 中。 可以选择指定要生成的根元素名称。 如果未指定可选的根名称，默认值\<根 > 元素添加。  
  
 有关详细信息，请参阅[FOR XML &#40;SQL server&#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
 **有关 XML 示例**  
  
 以下示例指定具有 `FOR XML AUTO` 和 `TYPE` 选项的 `XMLSCHEMA`。 由于`TYPE`选项，结果集返回到客户端作为**xml**类型。 `XMLSCHEMA` 选项指定在所返回的 XML 数据中包括内联 XSD 架构，而 `ELEMENTS` 选项指定 XML 结果是以元素为中心的。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT p.BusinessEntityID, FirstName, LastName, PhoneNumber AS Phone  
FROM Person.Person AS p  
JOIN Person.PersonPhone AS pph ON p.BusinessEntityID  = pph.BusinessEntityID  
WHERE LastName LIKE 'G%'  
ORDER BY LastName, FirstName   
FOR XML AUTO, TYPE, XMLSCHEMA, ELEMENTS XSINIL;  
```  
  
## <a name="for-json"></a>对于 JSON  
 JSON  
 指定 FOR JSON，来返回查询结果格式化为 JSON 文本。 你还必须指定以下 JSON 模式之一： 自动或路径。 有关详细信息**FOR JSON**子句，请参阅[查询结果格式化为 JSON 使用 FOR JSON &#40;SQL server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 AUTO  
 格式 JSON 输出自动基于的结构**选择**语句  
            通过指定**FOR JSON AUTO**。 有关详细信息和示例，请参阅[在 AUTO 模式下自动格式化 JSON 输出 (SQL Server)](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)。  
  
 PATH  
 通过指定获取对 JSON 输出格式的完全控制   
            **JSON 路径**。 借助**PATH** 模式，你可以创建包装器对象，并嵌套复杂属性。 有关详细信息和示例，请参阅[在 PATH 模式下设置嵌套的 JSON 输出格式 (SQL Server)](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)。  
  
 INCLUDE_NULL_VALUES  
 在 JSON 输出中包括 null 值，通过指定**INCLUDE_NULL_VALUES**选项与**FOR JSON**子句。 如果未指定此选项，输出不包括在查询结果中 null 值的 JSON 属性。 有关详细信息和示例，请参阅[使用 INCLUDE_NULL_VALUES 选项 &#40; 的 JSON 输出中包括 Null 值SQL server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).  
  
 ROOT [ **('***RootName***')** ]  
 将单个顶层元素添加到 JSON 输出中，通过指定**根**选项与**FOR JSON**子句。 如果没有指定 **ROOT** 选项，则 JSON 输出不会包括根元素。 有关详细信息和示例，请参阅[将根节点添加到使用 ROOT 选项 &#40; 的 JSON 输出SQL server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
 WITHOUT_ARRAY_WRAPPER  
 删除通过指定默认情况下环绕 JSON 输出的方括号**WITHOUT_ARRAY_WRAPPER**选项与**FOR JSON**子句。 如果不指定此选项，JSON 输出将括在方括号中。 使用**WITHOUT_ARRAY_WRAPPER**选项以生成单个 JSON 对象作为输出。  有关详细信息，请参阅 [使用 WITHOUT_ARRAY_WRAPPER 选项从 JSON 输出中删除方括号 (SQL Server)](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md)。  
  
 有关详细信息，请参阅[借助 FOR JSON 将查询结果格式化为 JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)  
  
  
