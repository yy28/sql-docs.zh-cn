---
title: "使用变量和参数 (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "参数 [MDX]"
  - "查询 [MDX], 变量"
  - "查询 [MDX], 参数"
  - "变量 [MDX]"
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 29
---
# 使用变量和参数 (MDX)
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，可以参数化多维表达式 (MDX) 语句。 参数化语句允许您创建可在运行时自定义的一般语句。  
  
 在创建参数化语句时，通过在参数名称前面添加 at 符号 (@) 来标识参数名称。 例如，@Year 是一个有效的参数名称。  
  
 MDX 仅支持文字值或标量值的参数。 若要创建引用成员、集或元组的参数，必须使用函数，如 [StrToMember](../../../mdx/strtomember-mdx.md) 或 [StrToSet](../../../mdx/strtoset-mdx.md)。  
  
 在下面的 XML for Analysis (XMLA) 示例中，@CountryName 参数将包含检索其客户数据的国家/地区。  
  
```  
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">  
  <Body>  
    <Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <Command>  
        <Statement>  
select [Measures].members on 0,   
       Filter(Customer.[Customer Geography].Country.members,   
              Customer.[Customer Geography].CurrentMember.Name =  
              @CountryName) on 1  
from [Adventure Works]  
</Statement>  
      </Command>  
      <Properties />  
      <Parameters>  
        <Parameter>  
          <Name>CountryName</Name>  
          <Value>'United Kingdom'</Value>  
        </Parameter>  
      </Parameters>  
    </Execute>  
  </Body>  
</Envelope>  
```  
  
 若要将此功能与 OLE DB 结合使用，请使用 **ICommandWithParameters** 接口。 若要将此功能与 ADOMD.Net 结合使用，请使用 **AdomdCommand.Parameters** 集合。  
  
## 另请参阅  
 [MDX 脚本编写基础知识 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  