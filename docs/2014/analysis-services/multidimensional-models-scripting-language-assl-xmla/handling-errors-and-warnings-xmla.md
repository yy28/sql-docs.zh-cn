---
title: 处理错误和警告 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- inline errors [XMLA]
- SOAP faults [XML for Analysis]
- XML for Analysis, errors
- faults [XML for Analysis]
- messages [XML for Analysis]
- XMLA, errors
- warnings [XML for Analysis]
- inline warnings [XMLA]
ms.assetid: ab895282-098d-468e-9460-032598961f45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 856886a5edfa5dcae604b44f5c2dca356ba0addb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702136"
---
# <a name="handling-errors-and-warnings-xmla"></a>处理错误和警告 (XMLA)
  错误处理时是必需的 XML for Analysis (XMLA) [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)或[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法调用不会运行，成功运行，但将生成错误或警告，或成功运行，但返回的结果包含错误的。  
  
|错误|报表|  
|-----------|---------------|  
|XMLA 方法调用不能运行|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 返回 SOAP 错误消息包含失败的详细信息。<br /><br /> 有关详细信息，请参阅部分中，[处理 SOAP 错误](#handling_soap_faults)。|  
|方法调用运行成功，但生成了错误或警告|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括[错误](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla)或[警告](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla)元素的每个错误或警告，分别在[消息](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)属性的[根](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla)元素包含方法调用的结果。<br /><br /> 有关详细信息，请参阅部分中，[处理错误和警告](#handling_errors_and_warnings)。|  
|方法调用运行成功，但结果中包含错误|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括内联`error`或`warning`元素的错误或警告，分别在适当[单元格](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)或[行](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla)元素的方法调用的结果。<br /><br /> 有关详细信息，请参阅部分中，[处理内联错误和警告](#handling_inline_errors_and_warnings)。|  
  
##  <a name="handling_soap_faults"></a> 处理 SOAP 错误  
 出现以下情况时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会返回 SOAP 错误：  
  
-   包含 XMLA 方法的 SOAP 消息格式不正确，或者无法由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例验证。  
  
-   出现与包含 XMLA 方法的 SOAP 消息有关的通信错误或其他错误。  
  
-   XMLA 方法未在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上运行。  
  
 XMLstartA 的 SOAP 错误代码以“XMLForAnalysis”开头，后跟一个句号和十六进制的 HRESULT 结果代码。 例如，错误代码“`0x80000005`”的格式为“`XMLForAnalysis.0x80000005`”。 有关 SOAP 错误格式的详细信息，请参阅“W3C 简单对象访问协议 (SOAP) 1.1. 中的 SOAP 错误”。  
  
### <a name="fault-code-information"></a>错误代码信息  
 下表显示了 SOAP 响应详细信息部分包含的 XMLA 错误代码信息。 这些列为 SOAP 错误详细信息部分中所包含的错误的属性。  
  
|列名|类型|Description|允许 null<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|指示方法是成功还是失败的返回代码。 十六进制值必须转换为 `UnsignedInt` 值。|否|  
|`WarningCode`|`UnsignedInt`|指示警告条件的返回代码。 十六进制值必须转换为 `UnsignedInt` 值。|是|  
|`Description`|`String`|由生成错误的组件返回的错误或警告的文本和说明。|是|  
|`Source`|`String`|生成错误或警告的组件的名称。|是|  
|`HelpFile`|`String`|指向介绍错误或警告的“帮助”文件或主题的路径或 URL。|是|  
  
 <sup>1</sup>指示是否将数据是必需的并且必须返回，或是否数据是可选的如果列不适用于允许使用 null 字符串。  
  
 下面列出了一个由于方法调用失败而出现的 SOAP 错误示例：  
  
```  
<?xml version="1.0"?>  
   <SOAP-ENV:Envelope  
   xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
   SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
      <SOAP-ENV:Fault>  
         <faultcode>XMLAnalysisError.0x80000005</faultcode>  
         <faultstring>The XML for Analysis provider encountered an error.</faultstring>  
         <faultactor>XML for Analysis Provider</faultactor>  
         <detail>  
<Error  
ErrorCode="2147483653"  
Description="An unexpected error has occurred."  
Source="XML for Analysis Provider"  
HelpFile="" />  
         </detail>  
      </SOAP-ENV:Fault>  
</SOAP-ENV:Envelope>  
```  
  
##  <a name="handling_errors_and_warnings"></a> 处理错误和警告  
 如果运行某命令后出现以下情况，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在该命令的 `Messages` 元素中返回 `root` 属性：  
  
-   该方法本身没有失败，但在该方法调用成功后，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上出现了错误。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例在该命令成功后返回一个警告。  
  
 `Messages` 属性出现在 `root` 元素中包含的所有其他属性之后，该属性可包含一个或多个 `Message` 元素。 而每个 `Message` 元素又可以包含一个 `error` 或 `warning` 元素，这些元素分别描述了指定命令产生的所有错误或警告。  
  
 有关错误和警告中包含的详细信息`Messages`属性，请参阅[Messages 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)。  
  
### <a name="handling-errors-during-serialization"></a>处理序列化期间发生的错误  
 如果错误发生后[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例已开始序列化的成功运行的命令，输出[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]返回[异常](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla)错误在不同的命名空间中的元素。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例随后会关闭所有已打开的元素，以确保发送到客户端的 XML 文档为有效文档。 该实例还会返回包含错误说明的 `Messages` 元素。  
  
##  <a name="handling_inline_errors_and_warnings"></a> 处理内联错误和警告  
 如果 XMLA 方法本身没有失败，但在 XMLA 方法调用成功后，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上出现了特定于该方法返回结果中的数据元素的错误，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会为命令返回内联 `error` 或 `warning`。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供内联`error`并`warning`元素问题特定于的单元格或其他数据是否包含在`root`元素使用[MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla)发生数据类型，如安全错误或格式设置该单元格的错误。 在这类情况下，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在包含错误或警告的 `error` 或 `warning` 元素中返回 `Cell` 或 `row` 元素。  
  
 下面的示例说明了结果集，其中包含在返回的行集时出错`Execute`方法使用[语句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令。  
  
```  
<return>  
   ...  
   <root>  
      ...  
      <CellData>  
      ...  
         <Cell CellOrdinal="10">  
            <Value>  
               <Error>  
                  <ErrorCode>2148497527</ErrorCode>   
                  <Description>Security Error.</Description>   
               </Error>  
            </Value>  
         </Cell>  
      </CellData>  
      ...  
   </root>  
   ...  
</return>  
```  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
