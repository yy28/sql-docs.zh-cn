---
title: 报表设计器的表达式中的自定义代码和程序集引用 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- items [Reporting Services], expressions
- data [Reporting Services], expressions
- expressions [Reporting Services], about expressions
- expressions [Reporting Services]
- SSRS, expressions
- formulas [Reporting Services]
- data manipulation [Reporting Services]
- SQL Server Reporting Services, expressions
ms.assetid: ae8a0166-2ccc-45f4-8d28-c150da7b73de
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 834fdb8af069a43f8c0ba1c3960d4516f8400767
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152857"
---
# <a name="custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs"></a>报表设计器的表达式中的自定义代码和程序集引用 (SSRS)
  您可以添加对报表中嵌入的自定义代码的引用，或添加对生成并保存到您的计算机并且部署到报表服务器的自定义程序集的引用。 对于自定义常量、复杂的函数，或在一个报表中多次使用的函数，可使用嵌入代码。 可以使用自定义代码程序集在一个位置中维护代码，并共享该代码以便由多个报表使用。 自定义代码可包含新的自定义常量、变量、函数或子例程。 可以包含对内置集合（例如，Parameters 集合）的只读引用。 但是，无法将报表数据值集传递给自定义函数；特别要指出的是，不支持自定义聚合。  
  
> [!IMPORTANT]  
>  对于在运行时计算一次以及希望在整个报表处理期间都保留相同值的时效性计算，请考虑使用报表变量或组变量。 有关详细信息，请参阅[报表和组变量集合引用（报表生成器和 SSRS）](built-in-collections-report-and-group-variables-references-report-builder.md)。  
  
 报表设计器是用于向报表中添加自定义代码的首选创作环境。 报表生成器支持处理具有有效表达式的报表，也支持处理包括对报表服务器上自定义程序集的引用的报表。 报表生成器不提供添加对自定义程序集的引用的方法。  
  
> [!NOTE]  
>  请注意，在报表服务器的升级过程中，依赖自定义程序集的报表可能需要额外的步骤才能完成升级。 有关详细信息，请参阅 [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RB3"></a> 在报表生成器中使用自定义代码  
 在报表生成器中，您可以从报表服务器中打开包含对自定义程序集的引用的报表。 例如，您可以编辑通过使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的报表设计器创建和部署的报表。 必须将自定义程序集部署到报表服务器。  
  
 您不能执行下列操作：  
  
1.  向报表中添加引用或类成员实例。  
  
2.  在本地模式下预览具有对自定义程序集的引用的报表。  
  
##  <a name="Common"></a> 包括对常用函数的引用  
 使用 **“表达式”** 对话框查看内置到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的常见函数分类列表。 展开 **“常见函数”** 并单击一个类别时， **“项”** 窗格显示表达式中包括的函数的列表。 常见函数包括 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.Math> 和 <xref:System.Convert> 命名空间和 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 运行时库函数的类。 为方便起见，您可以在 **“表达式”** 对话框中查看最常用的函数，这些函数按以下类别排列：文本、日期和时间、数学函数、检查函数、程序流函数、聚合函数、财务函数、转换函数和杂项函数。 不太常用的函数未显示在列表中，但仍然可以用在表达式中。  
  
 若要使用内置函数，请双击“项”窗格中的函数名称。 “说明”窗格中显示该函数的说明，“示例”窗格中显示函数调用的示例。 在“代码”窗格中，在左圆括号 **(** 后键入函数名称时，IntelliSense 将帮助显示函数调用的各项有效语法。 例如，若要计算表中一个名为 `Quantity` 的字段的最大值，首先将简单表达式 `=Max(` 添加到“代码”窗格，然后使用智能标记查看该函数调用的所有可能的有效语法。 若要完成本示例，请键入 `=Max(Fields!Quantity.Value)`。  
  
 有关每个函数的详细信息，请参阅 <xref:System.Math>、 <xref:System.Convert>和 MSDN 中的 [Visual Basic 运行时库成员](http://go.microsoft.com/fwlink/?LinkId=198941) 。  
  
##  <a name="NotCommon"></a> 包括对不太常用函数的引用  
 若要包括一个对不太常用的 CLR 命名空间的引用，必须使用完全限定引用，例如 <xref:System.Text.StringBuilder>。 对于这些不太常用的函数， **“表达式”** 对话框的“代码”窗格不支持 IntelliSense。  
  
 有关详细信息，请参阅 [Visual Basic Runtime Library Members](http://go.microsoft.com/fwlink/?LinkId=198941) （Visual Basic 运行时库成员）。  
  
##  <a name="External"></a> 包括对外部程序集的引用  
 若要包括对外部程序集中的类的引用，必须标识报表处理器的程序集。 使用 **“报表属性”** 对话框的 **“引用”** 页指定要添加到报表中的程序集的完全限定名称。 在表达式中，必须使用程序集中的类的完全限定名称。 外部程序集中的类不显示在 **“表达式”** 对话框中，您必须提供正确无误的类名称。 完全限定名称包括命名空间、类名称和成员名称。  
  
##  <a name="Embedded"></a> 包括嵌入代码  
 若要将嵌入代码添加到某个报表，请使用 **“报表属性”** 对话框的“代码”选项卡。 创建的代码块可以包含多个方法。 嵌入代码中的方法必须采用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 编写，并且必须是基于实例的方法。 对于 System.Convert 和 System.Math namespaces 命名空间，报表处理器会自动添加引用。 使用 **“报表属性”** 对话框的 **“引用”** 页添加其他程序集引用。 有关详细信息，请参阅[向报表添加程序集引用 (SSRS)](add-an-assembly-reference-to-a-report-ssrs.md)。  
  
 嵌入代码中的方法可通过全局定义的 `Code` 成员使用。 您可以访问这些参考`Code`成员和方法名称。 下面的示例调用方法`ToUSD`，它将转换中的值`StandardCost`字段为美元值：  
  
```  
=Code.ToUSD(Fields!StandardCost.Value)  
```  
  
 若要引用自定义代码中的内置集合，包含对内置的引用`Report`对象：  
  
```  
=Report.Parameters!Param1.Value  
```  
  
 下面的示例显示如何定义某些自定义常量和变量。  
  
```  
Public Const MyNote = "Authored by Bob"  
Public Const NCopies As Int32 = 2  
Public Dim  MyVersion As String = "123.456"  
Public Dim MyDoubleVersion As Double = 123.456  
```  
  
 尽管自定义常量不会出现在 **“表达式”** 对话框的 **“常量”** 类别（仅显示内置常量）中，但是可以从任何表达式向其中添加引用，如下面的示例所示。 在表达式中，自定义常量被视为`Variant`。  
  
```  
=Code.MyNote  
=Code.NCopies  
=Code.MyVersion  
=Code.MyDoubleVersion  
```  
  
 下面的示例包含的代码引用和代码实现函数`FixSpelling`，文本替换`"Bicycle"`所有出现的文本中"bike"`SubCategory`字段。  
  
 `=Code.FixSpelling(Fields!SubCategory.Value)`  
  
 嵌入报表定义代码块后，以下代码显示 `FixSpelling` 方法的实现。 此示例演示如何使用对的完全限定的引用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] `StringBuilder`类。  
  
```vb  
Public Function FixSpelling(ByVal s As String) As String  
   Dim strBuilder As New System.Text.StringBuilder(s)  
   If s.Contains("Bike") Then  
      strBuilder.Replace("Bike", "Bicycle")  
      Return strBuilder.ToString()  
      Else : Return s  
   End If  
End Function  
```  
  
 有关内置对象集合和初始化的详细信息，请参阅[内置的全局和用户引用（报表生成器和 SSRS）](built-in-collections-built-in-globals-and-users-references-report-builder.md)和[初始化自定义程序集对象](../custom-assemblies/initializing-custom-assembly-objects.md)。  
  
##  <a name="Parameters"></a> 包括对代码中的参数的引用  
 可以通过所提供的报表定义代码块中或自定义程序集中的自定义代码来引用全局参数集合。 该参数集合是只读的，并且没有公共迭代器。 不能使用[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]`For Each`步集合构造。 您需要首先知道在报表定义中定义的参数名称，然后才能在代码中引用该参数。 但是，可以遍历多值参数的所有值。  
  
 下表包含从自定义代码引用该内置集合 `Parameters` 的示例：  
  
|Description|表达式中的引用|自定义代码定义|  
|-----------------|-----------------------------|----------------------------|  
|将整个全局参数集合传递给自定义代码。<br /><br /> 该函数会返回特定报表参数 *MyParameter*的值。|`=Code.DisplayAParameterValue(Parameters)`|`Public Function DisplayAParameterValue(`<br /><br /> `ByVal parameters as Parameters) as Object`<br /><br /> `Return parameters("MyParameter").Value`<br /><br /> `End Function`|  
|将单个参数传递给自定义代码。<br /><br /> 此示例返回传入的参数的值。 如果该参数是多值参数，则返回字符串将是所有值的串联。|`=Code.ShowParametersValues(Parameters!DayOfTheWeek)`|`Public Function ShowParameterValues(ByVal parameter as Parameter)` <br />  `as String` <br /> `Dim s as String`  <br />  `If parameter.IsMultiValue then` <br />  `s = "Multivalue: "`  <br /> `For i as integer = 0 to parameter.Count-1` <br />  `s = s + CStr(parameter.Value(i)) + " "`  <br />  `Next` <br /> `Else` <br /> `s = "Single value: " + CStr(parameter.Value)` <br /> `End If` <br />  `Return s` <br /> `End Function`|  
  
##  <a name="Custom"></a> 包括对自定义程序集中的代码的引用  
 若要在报表中使用自定义程序集，您必须先创建程序集，使其可供报表设计器使用，然后在报表中添加对该程序集的引用，最后在报表中使用表达式来引用该程序集中包含的方法。 如果报表部署到报表服务器，您还必须向报表服务器部署该自定义程序集。  
  
 有关创建自定义的程序集并使其可供[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，请参阅[使用的报表的自定义程序集](../custom-assemblies/using-custom-assemblies-with-reports.md)。  
  
 若要在表达式中引用自定义代码，您必须调用程序集中某个类的成员。 调用方式取决于该方法是静态方法还是基于实例的方法。 自定义程序集中的静态方法可在报表内全局使用。 您可以在表达式中通过指定命名空间、类和方法名称来访问静态方法。 下面的示例调用方法`ToGBP`，它将转换的值**StandardCost**值从美元为英镑：  
  
```  
=CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
```  
  
 基于实例的方法可通过全局定义的 `Code` 成员使用。 您可以通过先引用 `Code` 成员，再引用实例和方法名称，来访问这些方法。 下面的示例调用实例方法`ToEUR`，它将转换的值**StandardCost**从美元改为欧元：  
  
```  
=Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
```  
  
> [!NOTE]  
>  在报表设计器中，除非您关闭 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，否则一旦加载自定义程序集，就不会卸载该程序集。 如果预览报表后对报表所用的自定义程序集进行更改，然后再次预览该报表，则第二次预览结果中不会体现所做的更改。 若要重新加载程序集，请关闭 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，再将其重新打开，然后预览报表。  
  
 有关访问代码的详细信息，请参阅 [Accessing Custom Assemblies Through Expressions](../custom-assemblies/accessing-custom-assemblies-through-expressions.md)。  
  
##  <a name="collections"></a> 将内置集合传递到自定义程序集  
 如果要将内置集合（如 *Globals* 或 *Parameters* 集合）传递到自定义程序集进行处理，则必须将代码项目中的程序集引用添加到定义内置集合的程序集中并且访问正确的命名空间。 根据您是为运行在报表服务器上的报表（服务器报表）开发自定义程序集，还是为在 .NET 应用程序中本地运行的报表（本地报表）开发自定义程序集，需要引用的程序集会有所不同。 有关详细信息，请参阅下面的内容。  
  
-   **命名空间：** Microsoft.ReportingServices.ReportProcessing.ReportObjectModel  
  
-   **程序集（本地报表）：** Microsoft.ReportingServices.ProcessingObjectModel.dll  
  
-   **程序集（服务器报表）：** Microsoft.ReportViewer.ProcessingObjectModel.dll  
  
 因为 *Fields* 和 *ReportItems* 集合的内容可在运行时动态更改，所以不应阻止它们对自定义程序集的调用（例如，在成员变量中）。 同样的建议通常应用于所有内置集合。  
  
## <a name="see-also"></a>请参阅  
 [向报表添加代码&#40;SSRS&#41;](add-code-to-a-report-ssrs.md)   
 [将自定义程序集用于报表](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [向报表添加程序集引用 (SSRS)](add-an-assembly-reference-to-a-report-ssrs.md)   
 [Reporting Services 教程 (SSRS)](../reporting-services-tutorials-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [报表示例（报表生成器和 SSRS）](http://go.microsoft.com/fwlink/?LinkId=198283)  
  
  
