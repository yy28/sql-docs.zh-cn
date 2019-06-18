---
title: 使用报表查看器控件集成 Reporting Services | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
helpviewer_keywords:
- Report Viewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8ffaeb12bc961256959571d18808e2869a1d7485
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62741870"
---
# <a name="integrating-reporting-services-using-report-viewer-controls"></a>使用报表查看器控件集成 Reporting Services
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2015 提供两个报表查看器控件，用于将报表查看功能集成到应用程序中。 一个控件版本针对基于 Windows 窗体的应用程序，另一个版本针对 Web 窗体应用程序。 每个控件都提供类似的功能，但分别设计为针对其各自的环境。 这两个控件都可以处理已部署到报表服务器（远程处理模式）的报表或已复制到尚未安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的计算机（本地处理模式）的报表。  
  
 报表查看器控件不包括对动态适应具有不同屏幕分辨率的不同设备的内置支持。  
  
## <a name="remote-processing-mode"></a>远程处理模式  
 远程处理模式是用于查看已部署到某一报表服务器的报表的首选方法。 远程处理模式具备以下优点：  
  
-   远程处理为运行报表提供优化的解决方案，因为报表服务器处理该报表。  
  
-   因为所有处理均由报表服务器进行，所以，报表请求可由扩展部署中的多个报表服务器或在某一扩展方案中具有多个处理器的服务器处理。  
  
 此外，在远程模式下运行的报表可利用报表服务器的全部功能，包括所有呈现和数据扩展插件。  
  
> [!NOTE]  
>  当该控件在远程处理模式下运行时可用于报表查看器控件的扩展插件的列表取决于在报表服务器上安装的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的版本。  
  
## <a name="local-processing-mode"></a>本地处理模式  
 本地处理模式提供在未安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 时用于查看和呈现报表的替代方法。 与远程处理不同，在该控件中只有报表服务器提供的一部分功能可用。 在本地处理模式中，数据处理不是由该控件处理的，而是由宿主应用程序实现的。 但是，报表处理由控件本身处理。 在本地处理模式中，只有 PDF、Excel、Word 和图像呈现扩展插件才可用。  
  
## <a name="see-also"></a>另请参阅  
 [将 Reporting Services 集成到应用程序中](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [使用 WebForms 报表查看器控件](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)   
 [使用 WinForms 报表查看器控件](../../reporting-services/application-integration/using-the-winforms-reportviewer-control.md)  

  
  
