---
title: "引用的 RDL 文件中的程序集 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 9fd80c818f13972434b72a72ce306e2f494cf56f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="referencing-assemblies-in-an-rdl-file"></a>在 RDL 文件中引用程序集
  若要支持使用自定义代码程序集在报表定义文件中，两个报表定义语言 (RDL) 元素都将纳入 RDL 规范： **CodeModules**元素和**类**元素。  
  
 **CodeModules**元素，您可以在报表表达式中的托管的代码程序集引用。 **CodeModules**是顶级元素，它包含对你用于在报表定义文件中调用专用的函数的程序集的引用。 支持使用自定义程序集的报表定义中的一个条目可能如下所示：  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 而不是调用<xref:System.Reflection.Assembly.Load%2A>任一手动添加，自定义代码，从注册你的自定义程序集**CodeModule**元素为 RDL 文件或通过使用**引用**选项卡**报表属性**对话框。 有关详细信息，请参阅[报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
 **类**元素支持报表定义中使用的实例成员。 **类**是顶级元素，它包含对类名称和实例名称的引用。 支持使用实例成员的报表定义中的一个条目可能如下所示：  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 有关详细信息，请参阅[通过表达式访问自定义程序集](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [将自定义程序集用于报表](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
