---
title: "通过表达式访问自定义程序集 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
- expressions [Reporting Services], custom assemblies
- static member calls
- instance member calls [Reporting Services]
- calling class members
- custom assemblies [Reporting Services], expressions
ms.assetid: 917c4d47-1a95-4f54-98b1-e8cb2165d90f
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 70ff488827e5289d401bf62b67a82a08ecc25f70
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="accessing-custom-assemblies-through-expressions"></a>通过表达式访问自定义程序集
  在创建自定义程序集、使其可用于报表设计器或报表服务器、添加适当的安全策略以及在报表定义中添加对自定义程序集的引用之后，您就可以使用报表表达式访问程序集中类的成员。 若要在表达式中引用自定义代码，您必须调用程序集中某个类的成员。 调用方式取决于该方法是静态方法还是基于实例的方法。  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>从报表定义文件调用静态成员  
 静态成员属于类或类型本身，而不属于实例化的对象。 可以通过从类中调用这些成员直接访问它们。 应尽可能使用静态成员在报表中调用自定义函数，因为静态成员的效果最佳。 若要调用的静态成员，你需要引用作为表达式，采用的形式 =*Namespace.Class.Method*。  
  
#### <a name="to-call-static-members"></a>调用静态成员  
  
-   若要调用静态成员，请将表达式设置为等于成员的完全限定名称（包括命名空间、类名称和成员名称）。 下面的示例调用**ToGBP**方法，后者将转换**StandardCost**字段值从美元为英镑并将其显示在报表中：  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>有关静态字段和属性的重要信息  
 目前，所有报表都在同一个应用程序域中执行。 这意味着具有用户特定的静态数据的报表将向同一报表的其他实例公开此数据。 这种情况可能会使一个用户的静态数据可用于当前运行特定报表的所有用户。 因此，强烈建议你不使用静态字段或属性中自定义程序集或在**代码**元素; 相反，在报表中使用实例字段或属性。 仍可以使用静态方法，因为它们不存储状态或数据。  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>从报表定义文件调用实例成员  
 如果您的自定义程序集包含您在报表定义中需要访问的实例成员，则必须将类的实例名称添加到报表中。 你可以添加类使用的实例名称**代码**选项卡**报表属性**对话框。 有关将类的实例添加到报表的详细信息，请参阅[自定义代码和在报表设计器 &#40; 中的表达式的程序集引用SSRS &#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 若要调用的静态成员，你需要引用作为表达式，采用的形式 = 代码*。InstanceName.Method*。  
  
#### <a name="to-call-instance-members"></a>调用实例成员  
  
-   若要调用的自定义程序集的实例成员，则必须引用**代码**关键字后跟实例名称和方法。 下面的示例调用实例方法**ToEUR**哪些将**StandardCost**字段值从美元为欧元并将其显示在报表中：  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [与报表中使用自定义程序集](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
