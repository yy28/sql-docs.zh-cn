---
title: 处理错误和警告 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 884474398abc9f449e5f6bd82c9f4b981f9a3a43
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144922"
---
# <a name="handling-errors-and-warnings-xmla"></a>处理错误和警告 (XMLA)
  错误处理时是必需的 XML for Analysis (XMLA) [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)或[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法调用不会运行，成功运行，但将生成错误或警告，或成功运行，但返回的结果包含错误的。  
  
|错误|报表|  
|-----------|---------------|  
|XMLA 方法调用不能运行|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 返回 SOAP 错误消息包含失败的详细信息。<br /><br /> 有关详细信息，请参阅部分中，[处理 SOAP 错误](#handling_soap_faults)。|  
|方法调用运行成功，但生成了错误或警告|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括[错误](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla)或[警告](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla)元素的每个错误或警告，分别在[消息](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)属性的[根](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla)元素包含方法调用的结果。<br /><br /> 有关详细信息，请参阅部分中，[处理错误和警告](#handling_errors_and_warnings)。|  
|方法调用运行成功，但结果中包含错误|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括内联**错误**或**警告**元素的错误或警告，分别在适当[单元格](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)或[行](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla)方法调用结果的元素。<br /><br /> 有关详细信息，请参阅部分中，[处理内联错误和警告](#handling_inline_errors_and_warnings)。|  
  
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
|**ErrorCode**|**UnsignedInt**|指示方法是成功还是失败的返回代码。 十六进制值必须可转换为**UnsignedInt**值。|否|  
|**WarningCode**|**UnsignedInt**|指示警告条件的返回代码。 十六进制值必须可转换为**UnsignedInt**值。|用户帐户控制|  
|**Description**|**String**|由生成错误的组件返回的错误或警告的文本和说明。|用户帐户控制|  
|**数据源**|**String**|生成错误或警告的组件的名称。|用户帐户控制|  
|**HelpFile**|**String**|指向介绍错误或警告的“帮助”文件或主题的路径或 URL。|用户帐户控制|  
  
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
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 返回**消息**属性中的**根**如果该命令运行后，会发生以下情况下为命令的元素：  
  
-   该方法本身没有失败，但在该方法调用成功后，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上出现了错误。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例在该命令成功后返回一个警告。  
  
 **消息**属性遵循所包含的所有其他属性**根**元素，并且可以包含一个或多个**消息**元素。 接下来，每个**消息**元素可以包含单个**错误**或**警告**分别描述任何错误或警告，针对发生的元素指定的命令。  
  
 有关错误和警告中包含的详细信息**消息**属性，请参阅[Messages 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla)。  
  
### <a name="handling-errors-during-serialization"></a>处理序列化期间发生的错误  
 如果错误发生后[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例已开始序列化的成功运行的命令，输出[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]返回[异常](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla)错误在不同的命名空间中的元素。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例随后会关闭所有已打开的元素，以确保发送到客户端的 XML 文档为有效文档。 实例也会返回**消息**元素，其中包含错误的说明。  
  
##  <a name="handling_inline_errors_and_warnings"></a> 处理内联错误和警告  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 返回内联**错误**或**警告**命令如果 XMLA 方法本身没有失败，但发生错误特定于该方法返回的结果中的数据元素[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]XMLA 方法调用成功后的实例。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供内联**错误**并**警告**元素问题特定于的单元格或其他数据是否包含在**根**元素使用[MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla)发生数据类型，如安全错误或该单元格的格式设置错误。 在这些情况下，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]将返回**错误**或**警告**中的元素**单元格**或**行**元素包含错误或警告，分别。  
  
 下面的示例说明了结果集，其中包含在返回的行集时出错**Execute**方法使用[语句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
