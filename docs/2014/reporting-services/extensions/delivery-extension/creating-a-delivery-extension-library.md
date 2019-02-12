---
title: 创建传递扩展插件库 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 63b32f93-4bab-4b07-bd72-39a47aca1cda
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ca393776d712eabea11eab07c08fa505105363c0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017168"
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
  
 当编译 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件时，因为此处包含传递扩展插件接口和类，所以您必须向编译器提供对于 Microsoft.ReportingServices.Interfaces.dll 的引用。 <xref:Microsoft.ReportingServices.Interfaces> 命名空间是实现 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 接口、<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 接口等所需的。 例如，如果所有文件（其中包含实现以 C# 编写的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 传递扩展插件的代码）都位于扩展名为 .cs 的单个目录中，则将从该目录发出以下命令，以编译存储在 CompanyName.ExtensionName.dll 中的文件。  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 以下代码示例说明可用于扩展名为 .vb 的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 文件的命令。  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  还可以使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 设计、开发和生成传递扩展插件。 有关在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中开发程序集的详细信息，请参阅 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 文档。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 扩展插件](../reporting-services-extensions.md)   
 [实现传递扩展插件](implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
