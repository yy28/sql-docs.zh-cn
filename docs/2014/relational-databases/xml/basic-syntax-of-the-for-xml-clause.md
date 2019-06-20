---
title: FOR XML 子句的基本语法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- BINARY BASE64 directive
- ROOT directive
- FOR XML clause, BINARY BASE64 directive
- FOR XML clause, syntax
- FOR XML clause, ROOT directive
ms.assetid: df19ecbf-d28e-4e9c-aaa3-700f8bbd3be4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0bb04374ede05406fdf6d273a76a246bb35f5dac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62637862"
---
# <a name="basic-syntax-of-the-for-xml-clause"></a>FOR XML 子句的基本语法
  FOR XML 模式可以是 RAW、AUTO、EXPLICIT 或 PATH。 它确定产生的 XML 的形状。  
  
> [!IMPORTANT]  
>  不推荐使用 FOR XML 选项的 XMLDATA 指令。 如果是 RAW 和 AUTO 模式，请使用 XSD 生成。 在 EXPLICT 模式下，没有可以代替 XMLDATA 指令的项。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 下面是 [FOR 子句 (Transact-SQL)](/sql/t-sql/queries/select-for-clause-transact-sql)中所述的基本语法：  
  
```  
[ FOR { BROWSE | <XML> } ]  
<XML> ::=  
XML   
    {   
      { RAW [ ('ElementName') ] | AUTO }   
        [   
           <CommonDirectives>   
           [ , { XMLDATA | XMLSCHEMA [ ('TargetNameSpaceURI') ]} ]   
           [ , ELEMENTS [ XSINIL | ABSENT ]   
        ]  
      | EXPLICIT   
        [   
           <CommonDirectives>   
           [ , XMLDATA ]   
        ]  
      | PATH [ ('ElementName') ]   
        [   
           <CommonDirectives>   
           [ , ELEMENTS [ XSINIL | ABSENT ] ]  
        ]  
     }   
  
 <CommonDirectives> ::=   
   [ , BINARY BASE64 ]  
   [ , TYPE ]  
   [ , ROOT [ ('RootName') ] ]  
```  
  
## <a name="arguments"></a>参数  
 RAW[('*ElementName*')]  
 采用查询结果并将结果集中的每一行转换为将通用标识符 \<row /> 作为元素标记的 XML 元素。 使用此指令时，可以选择指定行元素的名称。 产生的 XML 将把指定的 *ElementName* 用作为每行生成的行元素。 有关详细信息，请参阅 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)。  
  
 AUTO  
 以简单的嵌套 XML 树返回查询结果。 FROM 子句中的每个表（在 SELECT 子句中至少为其列出了一列）都表示为一个 XML 元素。 SELECT 子句中列出的列映射到适当的元素属性。 有关详细信息，请参阅 [将 AUTO 模式与 FOR XML 一起使用](use-auto-mode-with-for-xml.md)。  
  
 EXPLICIT  
 指定显式定义产生的 XML 树的形状。 使用此模式时，必须以一种特定的方式编写查询，以便显式指定所需嵌套的其他信息。 有关详细信息，请参阅 [将 EXPLICIT 模式与 FOR XML 一起使用](use-explicit-mode-with-for-xml.md)。  
  
 PATH  
 提供一种更简单的方式来混合元素和属性，并引入表示复杂属性的其他嵌套。 可以使用 FOR XML EXPLICIT 模式查询从行集中构造这种 XML，但 PATH 模式针对可能很烦琐的 EXPLICIT 模式查询提供了一种更简单的替代方式。 通过 PATH 模式，以及用于编写嵌套 FOR XML 查询的功能和返回 **xml** 类型实例的 TYPE 指令，您可以编写简单的查询。 它为编写大多数 EXPLICIT 模式查询提供了一个替代方式。 默认情况下，PATH 模式为结果集中的每一行生成一个 \<row> 元素包装。 您还可以选择指定元素名称。 如果这样，则指定的名称用作包装元素名称。 如果提供空字符串 (FOR XML PATH (''))，则不会生成任何包装元素。 有关详细信息，请参阅 [将 PATH 模式与 FOR XML 一起使用](use-path-mode-with-for-xml.md)。  
  
 XMLDATA  
 指定应返回内联 XML 数据简化 (XDR) 架构。 文档的架构被预置为内联架构。 有关工作示例，请参阅 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)。  
  
 XMLSCHEMA  
 返回内联 W3C XML 架构 (XSD)。 指定此指令时，可以选择指定目标命名空间 URI。 这样将返回架构中指定的命名空间。 有关详细信息，请参阅 [生成内联 XSD 架构](generate-an-inline-xsd-schema.md)。 有关工作示例，请参阅 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)。  
  
 ELEMENTS  
 如果指定 ELEMENTS 选项，则列作为子元素返回。 否则，列将映射到 XML 属性。 只在 RAW、AUTO 和 PATH 模式中支持此选项。 使用此指令时，可以选择指定 XSINIL 或 ABSENT。 XSINIL 指定为 NULL 列值创建 **xsi:nil** 属性设置为 True 的元素。 默认情况下，或者与 ELEMENTS 一起指定了 ABSENT 时，不会为 NULL 值创建任何元素。 有关工作示例，请参阅 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md) 和 [将 AUTO 模式与 FOR XML 一起使用](use-auto-mode-with-for-xml.md)。  
  
 BINARY BASE64  
 如果指定 BINARY Base64 选项，则查询所返回的任何二进制数据都用 base64 编码格式表示。 若要使用 RAW 和 EXPLICIT 模式检索二进制数据，必须指定此选项。 在 AUTO 模式中，默认情况下将二进制数据作为引用返回。 有关工作示例，请参阅 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)。  
  
 TYPE  
 指定查询以 **xml** 类型返回结果。 有关详细信息，请参阅 [TYPE Directive in FOR XML Queries](type-directive-in-for-xml-queries.md)。  
  
 ROOT [('*RootName*')]  
 指定向产生的 XML 中添加单个顶级元素。 可以选择指定要生成的根元素名称。 默认值为“root”。  
  
## <a name="see-also"></a>请参阅  
 [将 RAW 模式与 FOR XML 一起使用](use-raw-mode-with-for-xml.md)   
 [将 AUTO 模式与 FOR XML 一起使用](use-auto-mode-with-for-xml.md)   
 [将 EXPLICIT 模式与 FOR XML 一起使用](use-explicit-mode-with-for-xml.md)   
 [将 PATH 模式与 FOR XML 一起使用](use-path-mode-with-for-xml.md)   
 [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML (SQL Server)](for-xml-sql-server.md)  
  
  
