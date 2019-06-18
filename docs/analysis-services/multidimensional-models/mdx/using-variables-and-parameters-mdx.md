---
title: 使用变量和参数 (MDX) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: deb1f7b4e641dd2347e8629e1e13ad3f4da7788c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62989370"
---
# <a name="using-variables-and-parameters-mdx"></a>使用变量和参数 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中，可以参数化多维表达式 (MDX) 语句。 参数化语句允许您创建可在运行时自定义的一般语句。  
  
 在创建参数化语句时，通过在参数名称前面添加 at 符号 (@) 来标识参数名称。 例如，@Year是有效的参数名称  
  
 MDX 仅支持文字值或标量值的参数。 若要创建引用成员、集或元组的参数，必须使用函数，如 [StrToMember](../../../mdx/strtomember-mdx.md) 或 [StrToSet](../../../mdx/strtoset-mdx.md)。  
  
 在下面的 XML for Analysis (XMLA) 示例中，@CountryName参数将包含有关哪个客户检索数据的国家/地区：  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 脚本编写基础知识 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
