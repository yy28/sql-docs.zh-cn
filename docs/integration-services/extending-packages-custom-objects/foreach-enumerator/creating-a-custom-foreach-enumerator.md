---
title: "创建自定义 Foreach 枚举器 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom foreach enumerators [Integration Services], creating
ms.assetid: 050e8455-2ed0-4b6d-b3ea-4e80e6c28487
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f2f852ff319554d0b863fd06d790c2e5e9bf2d59
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-foreach-enumerator"></a>创建自定义 Foreach 枚举器
  创建自定义 foreach 枚举器的步骤与创建其他任何 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 自定义对象的步骤相似。  
  
-   创建一个从基类继承的新类。 对于 foreach 枚举器，基类是 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>。  
  
-   将标识对象类型的属性应用于该类。 对于 foreach 枚举器，该属性为 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>。  
  
-   重写基类的方法和属性的实现。 对于 foreach 枚举器，最重要的是 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 方法。  
  
-   可以选择开发自定义用户界面。 对于 foreach 枚举器，这需要实现 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSForEachEnumeratorUI> 接口的类。  
  
 自定义枚举器由 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 容器承载。 在运行时，<xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 容器会调用自定义枚举器的 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 方法。 自定义的枚举器返回的对象实现**IEnumerable**接口，如**ArrayList**。 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 随后循环访问该集合中的每个元素，并通过一个用户定义的变量将当前元素的值提供给控制流，然后在容器中执行控制流。  
  
## <a name="getting-started-with-a-custom-foreach-enumerator"></a>自定义 ForEach 枚举器入门  
  
### <a name="creating-projects-and-classes"></a>创建项目和类  
 由于所有托管 foreach 枚举器都是从基类 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 派生的，因此创建自定义 foreach 枚举器的第一步是创建一个用您首选的托管编程语言编写的类库项目，然后创建一个从该基类继承的类。 在此派生类中重写基类的属性和方法可实现您的自定义功能。  
  
 在同一解决方案中，创建另一个类库项目，用于自定义用户界面。 为便于部署，推荐对用户界面使用单独的程序集，因为这样，您就可以分别更新和重新部署 foreach 枚举器或其用户界面。  
  
 将这两个项目配置为使用强名称密钥文件对在生成时产生的程序集进行签名。  
  
### <a name="applying-the-dtsforeachenumerator-attribute"></a>应用 DtsForEachEnumerator 属性  
 将 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 属性应用于您创建的类以将其标识为 foreach 枚举器。 此属性提供设计时信息，如 foreach 枚举器的名称和说明。 **名称**属性将出现在下拉列表中的可用的枚举器在**集合**选项卡**Foreach 循环编辑器**对话框。  
  
 使用 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> 属性链接 foreach 枚举器与其自定义用户界面。 若要获取此属性，你使用需要的公钥令牌**sn.exe-t**以显示从你想要用于对用户接口程序集进行签名的密钥对 (.snk) 文件的公钥令牌。  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Namespace Microsoft.Samples.SqlServer.Dts  
    <DtsForEachEnumerator(DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")> _   
    Public Class MyEnumerator  
     Inherits ForEachEnumerator  
        'Insert code here.  
    End Class  
End Namespace  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsForEachEnumerator( DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")]  
    public class MyEnumerator : ForEachEnumerator  
    {  
        //Insert code here.  
    }  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-enumerator"></a>生成、部署和调试自定义枚举器  
 在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中生成、部署和调试自定义 foreach 枚举器的步骤与其他自定义对象类型所需的步骤非常相似。 有关详细信息，请参阅[构建，Deploying，and Debugging Custom Objects](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。  
  
## <a name="see-also"></a>另請參閱  
 [编码的自定义 Foreach 枚举器](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)   
 [开发的自定义 ForEach 枚举器的用户界面](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  
