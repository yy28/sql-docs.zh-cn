---
title: 编写自定义 Foreach 枚举器代码 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom foreach enumerators [Integration Services], coding
ms.assetid: 279cf6de-d06f-40e7-b8ca-569310449f36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 84e1b606c9eedaf4ae1d4b8394b8bf8d2bdcb140
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768623"
---
# <a name="coding-a-custom-foreach-enumerator"></a>编写自定义 Foreach 枚举器代码
  创建继承自 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 基类的类并将 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 属性应用于该类后，必须重写基类的属性和方法的实现以提供自定义功能。  
  
 若要查看自定义枚举器的工作示例，请参阅[为自定义 ForEach 枚举器开发用户界面](developing-a-user-interface-for-a-custom-foreach-enumerator.md)。  
  
## <a name="initializing-the-enumerator"></a>初始化枚举器  
 可以重写 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.InitializeForEachEnumerator%2A> 方法以缓存对包中定义的连接管理器的引用，和缓存对事件接口（用于引发错误、警告和信息性消息）的引用。  
  
## <a name="validating-the-enumerator"></a>验证枚举器  
 重写 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> 方法以验证枚举器是否正确配置。 如果该方法返回 `Failure`，则枚举器和包含枚举器的包将不执行。 此方法的实现是特定于每个枚举器的，但如果枚举器依赖于 <xref:Microsoft.SqlServer.Dts.Runtime.Variable> 或 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 对象，则应该添加代码以验证这些对象存在于提供给方法的集合中。  
  
 下面的代码示例演示 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> 的实现，该接口用于检查在枚举器的属性中指定的变量。  
  
```csharp  
private string variableNameValue;  
  
public string VariableName  
{  
    get{ return this.variableNameValue; }  
    set{ this.variableNameValue = value; }  
}  
  
public override DTSExecResult Validate(Connections connections, VariableDispenser variableDispenser, IDTSInfoEvents infoEvents, IDTSLogging log)  
{  
    if (!variableDispenser.Contains(this.variableNameValue))  
    {  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + this.variableNameValue + " does not exist in the collection.", "", 0);  
            return DTSExecResult.Failure;  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Private variableNameValue As String  
  
Public Property VariableName() As String  
    Get   
         Return Me.variableNameValue  
    End Get  
    Set (ByVal Value As String)   
         Me.variableNameValue = value  
    End Set  
End Property  
  
Public Overrides Function Validate(ByVal connections As Connections, ByVal variableDispenser As VariableDispenser, ByVal infoEvents As IDTSInfoEvents, ByVal log As IDTSLogging) As DTSExecResult  
    If Not variableDispenser.Contains(Me.variableNameValue) Then  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + Me.variableNameValue + " does not exist in the collection.", "", 0)  
            Return DTSExecResult.Failure  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
## <a name="returning-the-collection"></a>返回集合  
 在执行期间，<xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 容器调用自定义枚举器的 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 方法。 在此方法中，枚举器创建并填充它的项集合，然后返回该集合。 然后 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 遍历集合中的所有项，并为集合中的每个项执行控制流。  
  
 下面的示例演示返回随机整数数组的 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 的实现。  
  
```csharp  
public override object GetEnumerator()  
{  
    ArrayList numbers = new ArrayList();  
  
    Random randomNumber = new Random(DateTime.Now);  
  
    for( int x=0; x < 100; x++ )  
        numbers.Add( randomNumber.Next());  
  
    return numbers;  
}  
```  
  
```vb  
Public Overrides Function GetEnumerator() As Object  
    Dim numbers As ArrayList =  New ArrayList()   
  
    Dim randomNumber As Random =  New Random(DateTime.Now)   
  
        Dim x As Integer  
        For  x = 0 To  100- 1  Step  x + 1  
        numbers.Add(randomNumber.Next())  
        Next  
  
    Return numbers  
End Function  
```  
  
![集成服务图标 （小）](../../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [创建自定义 Foreach 枚举器](creating-a-custom-foreach-enumerator.md)   
 [为自定义 ForEach 枚举器开发用户界面](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  
