---
title: "创建自定义连接管理器 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom connection managers [Integration Services], creating
ms.assetid: e83f8e02-ace4-42e0-b979-2f6be1460985
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c617741134c19c012f487bc00263c2e4b071810
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-connection-manager"></a>创建自定义连接管理器
  创建自定义连接管理器时必须遵循的步骤与创建任何其他 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 自定义对象的步骤相似。  
  
-   创建一个从基类继承的新类。 对于连接管理器，该基类为 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>。  
  
-   将标识对象类型的属性应用于该类。 对于连接管理器，该属性为 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>。  
  
-   重写基类的方法和属性的实现。 对于连接管理器，所涉及的属性和方法包括 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> 属性以及 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> 方法。  
  
-   可以选择开发自定义用户界面。 对于连接管理器，这需要一个实现 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI> 接口的类。  
  
> [!NOTE]  
>  内置于 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 的大多数任务、源和目标都只能与特定类型的内置连接管理器一起工作。 因此，不能使用内置任务和组件测试这些示例。  
  
## <a name="getting-started-with-a-custom-connection-manager"></a>自定义连接管理器入门  
  
### <a name="creating-projects-and-classes"></a>创建项目和类  
 由于所有托管连接管理器都派生自 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> 基类，因此创建自定义连接管理器的第一步是以您首选的托管编程语言创建一个类库项目，然后创建一个从该基类继承的类。 在此派生类中，你将重写的方法和属性的基类，来实现自定义功能。  
  
 在同一解决方案中，创建另一个类库项目，用于自定义用户界面。 为便于部署，建议对用户界面使用单独的程序集，因为这可使您分别更新和重新部署连接管理器或其用户界面。  
  
 将这两个项目配置为使用强名称密钥文件对在生成时产生的程序集进行签名。  
  
### <a name="applying-the-dtsconnection-attribute"></a>应用 DtsConnection 属性  
 对已创建的类应用 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> 属性，以将其标识为连接管理器。 此属性提供设计时信息，例如连接管理器的名称、说明和连接类型。 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.ConnectionType%2A>和**说明**属性对应于**类型**和**说明**中显示的列**添加 SSIS 连接管理器**对话框中，配置中的包的连接时显示[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]。  
  
 使用 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.UITypeName%2A> 属性将连接管理器链接到其自定义用户界面。 若要获取此属性，你使用需要的公钥令牌**sn.exe-t**以显示从你想要用于对用户接口程序集进行签名的密钥对 (.snk) 文件的公钥令牌。  
  
```vb  
<DtsConnection(ConnectionType:="SQLVB", _  
  DisplayName:="SqlConnectionManager (VB)", _  
  Description:="Connection manager for Sql Server", _  
  UITypeName:="SqlConnMgrUIVB.SqlConnMgrUIVB,SqlConnMgrUIVB,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")> _  
Public Class SqlConnMgrVB  
  Inherits ConnectionManagerBase  
  . . .  
End Class  
```  
  
```csharp  
[DtsConnection(ConnectionType = "SQLCS",  
  DisplayName = "SqlConnectionManager (CS)",  
  Description = "Connection manager for Sql Server",  
  UITypeName = "SqlConnMgrUICS.SqlConnMgrUICS,SqlConnMgrUICS,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")]  
public class SqlConnMgrCS :  
ConnectionManagerBase  
{  
  . . .  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-connection-manager"></a>生成、部署和调试自定义连接管理器  
 在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中生成、部署和调试自定义连接管理器的步骤与其他自定义对象类型所需的步骤相似。 有关详细信息，请参阅[构建，Deploying，and Debugging Custom Objects](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。    
  
## <a name="see-also"></a>另请参阅  
 [编码自定义连接管理器](../../../integration-services/extending-packages-custom-objects/connection-manager/coding-a-custom-connection-manager.md)   
 [开发的自定义连接管理器的用户界面](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)  
  
  

