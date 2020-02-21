---
title: 向报表添加代码 (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom code [Reporting Services]
- expressions [Reporting Services], code
- adding code
- reports [Reporting Services], code
ms.assetid: 00ef8fc6-99fe-49b2-8a22-7eb475881dc4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d66cb9fa3fdb3bdee5eb0f4fefbc282a9841f9a7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65582027"
---
# <a name="add-code-to-a-report-ssrs"></a>向报表添加代码 (SSRS)
  您可以在任何表达式中调用自己的自定义代码。 可以通过下列两种方式提供代码：  
  
-   直接在报表中使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 编写的嵌入代码。 如果代码引用非 <xref:System.Math> 或 <xref:System.Convert> 的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，必须向报表中添加引用。 有关详细信息，请参阅 [向报表添加程序集引用 (SSRS)](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md)。 有关可从代码中使用的其他引用的详细信息，请参阅[报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
-   使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]提供自定义代码程序集。 如果提供自定义程序集，则必须同时在创作报表的计算机上和查看报表的报表服务器上安装该自定义程序集。 有关详细信息，请参阅 [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)。  
  
### <a name="to-add-embedded-code-to-a-report"></a>向报表添加嵌入代码  
  
1.  在“设计”视图中，右键单击报表边框外的设计图面，然后单击“报表属性”   。  
  
2.  单击 **“代码”** 。  
  
3.  在 **“自定义代码”** 中键入代码。 报表运行时，代码中的错误会引发警告。 下面的示例创建一个名为 `ChangeWord` 的自定义函数，该函数可使用词语“`Bike`”替换“`Bicycle`”。  
  
    ```  
    Public Function ChangeWord(ByVal s As String) As String  
       Dim strBuilder As New System.Text.StringBuilder(s)  
       If s.Contains("Bike") Then  
          strBuilder.Replace("Bike", "Bicycle")  
          Return strBuilder.ToString()  
          Else : Return s  
       End If  
    End Function  
    ```  
  
4.  下面的示例演示如何在表达式中向此函数传递名为 Category 的数据集字段。  
  
    ```  
    =Code.ChangeWord(Fields!Category.Value)  
    ```  
  
     如果将此表达式添加到显示类别值的表单元，则只要该行的数据集字段中出现词语“Bike”，表单元值就会显示词语“Bicycle”。  
  
## <a name="see-also"></a>另请参阅  
 [“报表属性”对话框 -&gt;“代码”](https://msdn.microsoft.com/library/955d4b11-17b4-4f1c-9690-6e7af54caea7)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Parameters 集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
