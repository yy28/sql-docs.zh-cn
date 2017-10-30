---
title: "创建自定义日志提供程序 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- custom log providers [Integration Services], creating
ms.assetid: fc20af96-9eb8-4195-8d3f-8a4d7c753f24
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4e98f1b5a032353c27ffa1438eb7d01bd517892a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-log-provider"></a>创建自定义日志提供程序
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 运行时环境具有广泛的日志记录功能。 日志可使您捕获在包执行期间发生的事件。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含各种日志提供程序，可用于创建日志并以诸如 XML、文本、数据库或 Windows 事件日志的格式存储这些日志。 如果这些提供程序或输出格式不能满足您的需要，您可以创建自定义日志提供程序。  
  
 创建自定义日志提供程序的步骤与创建其他任何 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 自定义对象的步骤相似：  
  
-   创建一个从基类继承的新类。 对于日志提供程序，该基类为 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>。  
  
-   将标识对象类型的属性应用于该类。 对于日志提供程序，该属性为 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>。  
  
-   重写基类的方法和属性的实现。 对于日志提供程序，所涉及的属性和方法包括 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 属性以及 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 方法。  
  
-   未实现自定义日志提供程序的自定义用户界面[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]。  
  
## <a name="getting-started-with-a-custom-log-provider"></a>自定义日志提供程序入门  
  
### <a name="creating-projects-and-classes"></a>创建项目和类  
 由于所有托管日志提供程序都派生自 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 基类，所以创建自定义日志提供程序的第一步是以您的首选托管编程语言创建一个类库项目，然后创建一个从该基类继承的类。 在此派生类中重写基类的属性和方法可实现您的自定义功能。  
  
 将此项目配置为使用强名称密钥文件对将要生成的程序集进行签名。  
  
> [!NOTE]  
>  许多[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]日志提供程序具有实现的自定义用户界面<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI>，并替换**配置**文本框中**配置 SSIS 日志**与筛选的下拉列表的可用连接管理器的对话框。 但是，[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中不实现自定义日志提供程序的自定义用户界面。  
  
### <a name="applying-the-dtslogprovider-attribute"></a>应用 DtsLogProvider 属性  
 将 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 属性应用于您创建的类以将其标识为日志提供程序。 此属性提供设计时信息，如日志提供程序的名称和说明。 **DisplayName**和**说明**的属性的属性对应于**名称**和**说明**中显示的列**配置 SSIS 日志**编辑器中，配置中的包的日志记录时才会显示[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]。  
  
> [!IMPORTANT]  
>  不使用此特性的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.LogProviderType%2A> 属性。 但是，必须为该属性输入一个值，否则自定义日志提供程序将不会显示在可用日志提供程序列表中。  
  
> [!NOTE]  
>  由于自定义日志提供程序的自定义用户界面不在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中实现，因此，为 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 属性指定值将不起作用。  
  
```vb  
<DtsLogProvider(DisplayName:="MyLogProvider", Description:="A simple log provider.", LogProviderType:="Custom")> _  
Public Class MyLogProvider  
     Inherits LogProviderBase  
    ' TODO: Override the base class methods.  
End Class  
```  
  
```csharp  
[DtsLogProvider(DisplayName="MyLogProvider", Description="A simple log provider.", LogProviderType="Custom")]  
public class MyLogProvider : LogProviderBase  
{  
    // TODO: Override the base class methods.  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-log-provider"></a>生成、部署和调试自定义日志提供程序  
 在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中生成、部署和调试自定义日志提供程序的步骤与其他自定义对象类型所需的步骤非常相似。 有关详细信息，请参阅[构建，Deploying，and Debugging Custom Objects](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。  
  
## <a name="see-also"></a>另請參閱  
 [编码的自定义日志提供程序](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)   
 [开发的自定义日志提供程序的用户界面](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)  
  
  

