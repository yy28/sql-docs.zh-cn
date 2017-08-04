---
title: "Enhancing an Error Output with the Script Component |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 3881b57f4089dbb075d019f9bd1a88a96a307b72
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="enhancing-an-error-output-with-the-script-component"></a>使用脚本组件增强错误输出
  默认情况下中的两个额外列[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]ErrorCode 和 ErrorColumn，错误输出包含仅数字代码，可表示的错误号和发生错误的列的 ID。 这些数字的值可以是使用的有限，不必进行相应的错误说明和列的名称。  
  
 本主题介绍如何通过使用脚本组件添加到数据流中的数据的现有错误输出数据的错误说明和列名称。 示例使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 接口的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法添加与特定预定义 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 错误代码对应的错误说明，该接口通过脚本组件的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 属性提供。 然后该示例通过将对应的列名称添加到捕获的沿袭 ID<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A>同一接口的方法。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个数据流任务和多个包的组件，请考虑以此脚本组件示例中的代码为基础，创建自定义数据流组件。 有关详细信息，请参阅 [开发自定义数据流组件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="example"></a>示例  
 此处显示的示例使用配置转换为脚本组件将错误说明和列名称添加到数据流中的数据的现有错误输出数据。  
  
 有关如何将使用脚本组件配置为数据流中的数据转换的详细信息，请参阅[使用脚本组件创建同步转换](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)和[使用脚本组件创建异步转换](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。  
  
#### <a name="to-configure-this-script-component-example"></a>配置此脚本组件示例  
  
1.  创建新脚本组件之前，先配置数据流中的上游组件，以便在错误或截断出现时将行重定向到上游组件的错误输出。 出于测试目的，您可能希望以确保将发生错误的方式来配置组件，例如，在两个将发生查找失败的表之间配置一个查找转换。  
  
2.  向数据流设计器图面添加新的脚本组件并将其配置为转换。  
  
3.  将错误输出从上游组件连接到新脚本组件。  
  
4.  打开**脚本转换编辑器**，然后在**脚本**页上，为**ScriptLanguage**属性，选择的脚本语言。  
  
5.  单击**编辑脚本**以打开[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 并添加下面显示的示例代码。  
  
6.  关闭 VSTA。  
  
7.  在脚本转换编辑器中，在**输入列**页上，选择错误代码和 ErrorColumn 列。  
  
8.  上**输入和输出**页上，添加两个新列。  
  
    -   添加新的输出列的类型**字符串**名为**ErrorDescription**。 将新列的默认长度提高到 255 以支持长消息。  
  
    -   添加另一个新的输出列的类型**字符串**名为**ColumnName**。 增加到 255 之间以支持较长的值的新列的默认长度。  
  
9. 关闭**脚本转换编辑器。**  
  
10. 将脚本组件的输出连接到合适的目标。 对于即席测试，平面文件目标是最容易配置的。  
  
11. 运行包。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription = _  
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
      Dim componentMetaData130 = TryCast(Me.ComponentMetaData, IDTSComponentMetaData130)  
      If componentMetaData130 IsNot Nothing Then  
        Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn)  
         End If  
  
    End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
{  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
      Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
      var componentMetaData130 = this.ComponentMetaData as IDTSComponentMetaData130;  
      if (componentMetaData130 != null)  
        {  
            Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn);  
        }  
  
    }  
}  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)   
 [在数据流组件中使用错误输出](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [使用脚本组件创建同步转换](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  
