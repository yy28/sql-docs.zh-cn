---
title: 自定义报表项实现要求 | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0000e0c7a5933003544de22b60a8adc4d9c59c82
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74684447"
---
# <a name="custom-report-item-implementation-requirements"></a>自定义报表项实现要求
  本主题将讨论开发和部署自定义报表项的先决条件。  
  
## <a name="development-and-deployment-requirements"></a>开发和部署要求  
 为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 开发自定义报表项要求满足以下条件：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]运行的服务器的管理访问权限。  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)]或更高[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]版本安装了软件开发工具包（SDK）。  
  
-   对于 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档的访问权限。  
  
-   熟悉组件创作和 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的组件模型命名空间。 有关详细信息，请参阅 msdn.microsoft.com 上的“组件创作”和“Visual Studio 中的组件模型命名空间”。  
  
## <a name="language-and-namespace-requirements"></a>语言和命名空间要求  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自定义报表项完全支持 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。 您可以使用您选择的 .NET 兼容的语言开发自定义报表项。  
  
 
  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 为开发人员提供了许多工具和功能以简化和加速编码、调试和测试的迭代周期，并使部署过程更为容易。 
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 包括 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 和 C# 编译器以及相关工具。  
  
-   自定义报表项使用 `Microsoft.ReportDesigner` 和 <xref:Microsoft.ReportingServices.Interfaces> 命名空间。 它们存储在作为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的一部分安装的 Microsoft.ReportingServices.Designer.DLL 和 Microsoft.ReportingServices.Interfaces.DLL 程序集中。  
  
-   自定义报表项设计时组件需要在 <xref:System.ComponentModel> 中从 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 命名空间实现接口。 
  <xref:System.ComponentModel> SDK 文档中有关于 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的记载。  
  
> [!IMPORTANT]  
>  默认情况下，[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起安装，但不安装 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。 除非 SDK 已安装在计算机上，并且 SDK 文档包含在联机丛书集中，否则本部分中指向 SDK 内容的链接将无效。 安装 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 后，可以按照[添加或删除 SQL Server 的产品文档](../../2014-toc/index.yml)中的说明将 SDK 文档添加到联机丛书集和目录中。  
  
## <a name="see-also"></a>另请参阅  
 [创建自定义报表项运行时组件](creating-a-custom-report-item-run-time-component.md)   
 [创建自定义报表项设计时组件](creating-a-custom-report-item-design-time-component.md)   
 [如何：部署自定义报表项](how-to-deploy-a-custom-report-item.md)   
 [自定义报表项类库](custom-report-item-class-libraries.md)  
  
  
