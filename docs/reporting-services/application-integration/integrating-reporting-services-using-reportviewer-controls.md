---
title: "使用 ReportViewer 控件集成 Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ReportViewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
caps.latest.revision: "26"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: aca22faca7e80ef9fa509e934380f9168d156498
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="integrating-reporting-services-using-reportviewer-controls"></a>使用 ReportViewer 控件集成 Reporting Services
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2015 提供两个 ReportViewer 控件，用于将报表查看功能集成到应用程序中。 一个控件版本针对基于 Windows 窗体的应用程序，另一个版本针对 Web 窗体应用程序。 每个控件都提供类似的功能，但分别设计为针对其各自的环境。 这两个控件都可以处理已部署到报表服务器（远程处理模式）的报表或已复制到尚未安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的计算机（本地处理模式）的报表。  
  
 ReportViewer 控件不包括对动态适应具有不同屏幕分辨率的不同设备的内置支持。  
  
## <a name="remote-processing-mode"></a>远程处理模式  
 远程处理模式是用于查看已部署到某一报表服务器的报表的首选方法。 远程处理模式具备以下优点：  
  
-   远程处理为运行报表提供优化的解决方案，因为报表服务器处理该报表。  
  
-   因为所有处理均由报表服务器进行，所以，报表请求可由扩展部署中的多个报表服务器或在某一扩展方案中具有多个处理器的服务器处理。  
  
 此外，在远程模式下运行的报表可利用报表服务器的全部功能，包括所有呈现和数据扩展插件。  
  
> [!NOTE]  
>  当该控件在远程处理模式下运行时可用于 ReportViewer 控件的扩展插件的列表取决于在报表服务器上安装的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的版本。  
  
## <a name="local-processing-mode"></a>本地处理模式  
 本地处理模式提供在未安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 时用于查看和呈现报表的替代方法。 与远程处理不同，在该控件中只有报表服务器提供的一部分功能可用。 在本地处理模式中，数据处理不是由该控件处理的，而是由宿主应用程序实现的。 但是，报表处理由控件本身处理。 在本地处理模式中，只有 PDF、Excel、Word 和图像呈现扩展插件才可用。  
  
## <a name="see-also"></a>另请参阅  
 [将 Reporting Services 集成到应用程序中](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [使用 WebForms ReportViewer 控件](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)   
 [使用 WinForms ReportViewer 控件](../../reporting-services/application-integration/using-the-winforms-reportviewer-control.md)  

  
  
