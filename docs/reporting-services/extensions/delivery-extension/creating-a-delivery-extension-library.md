---
title: "创建传递扩展库 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- delivery extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 63b32f93-4bab-4b07-bd72-39a47aca1cda
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bcfb5b69df148108531e9e5b843f127af0e3fbb4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="creating-a-delivery-extension-library"></a>创建传递扩展插件库
  您创建的每个 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件都应分配到唯一的命名空间并被内置到某个库或程序集文件中。 命名空间的确切名称并不重要，但命名空间必须是唯一的且不能与任何其他扩展插件共享。 您应该为公司的传递扩展插件创建您自己的唯一命名空间。  
  
 以下示例说明开始某个 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件的代码，此扩展插件使用包含传递接口和任何实用工具类的命名空间。  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 当编译 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件时，因为此处包含传递扩展插件接口和类，所以您必须向编译器提供对于 Microsoft.ReportingServices.Interfaces.dll 的引用。 <xref:Microsoft.ReportingServices.Interfaces> 命名空间是实现 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 接口、<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 接口等所需的。 例如，如果所有包含来实现的代码的文件[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]用 C# 编写的传递扩展插件与扩展.cs 单个目录中，从该目录进行编译 CompanyName.ExtensionName.dll 中存储的文件，因此将发出以下命令。  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 下面的代码示例显示将用于命令[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]带有扩展名的文件。 vb.  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  还可以使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 设计、开发和生成传递扩展插件。 有关在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中开发程序集的详细信息，请参阅 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 文档。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

