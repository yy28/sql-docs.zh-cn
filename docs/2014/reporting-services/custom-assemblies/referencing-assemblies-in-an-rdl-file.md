---
title: 在 RDL 文件中引用程序集 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bc52419f382ea44fc718a47e99bbd0981275d240
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63264799"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>在 RDL 文件中引用程序集
  为了支持在报表定义文件中使用自定义代码程序集，RDL 规范中包含两个报表定义语言 (RDL) 元素：CodeModules 元素和 Classes 元素   。  
  
 通过 CodeModules 元素，可以在报表表达式中引用托管代码程序集  。 CodeModules 是一个顶级元素，它包含针对在报表定义文件中用来调用专用函数的程序集的引用  。 支持使用自定义程序集的报表定义中的一个条目可能如下所示：  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 可以通过手动将 CodeModule 元素添加到 RDL 文件或使用“报表属性”对话框的“引用”选项卡来注册自定义程序集，而不是从自定义代码调用 <xref:System.Reflection.Assembly.Load%2A>    。 有关详细信息，请参阅 [报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
 Classes 元素支持在报表定义中使用实例成员  。 Classes 是一个顶级元素，它包含对类名称和实例名称的引用  。 支持使用实例成员的报表定义中的一个条目可能如下所示：  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 有关详细信息，请参阅[通过表达式访问自定义程序集](accessing-custom-assemblies-through-expressions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [将自定义程序集用于报表](using-custom-assemblies-with-reports.md)  
  
  
