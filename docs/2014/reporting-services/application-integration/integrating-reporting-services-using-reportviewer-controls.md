---
title: 使用 ReportViewer 控件集成 Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ReportViewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
caps.latest.revision: 23
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0d8ecc6116b5000c1db7100abf4ea4db5155ca7f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37317987"
---
# <a name="integrating-reporting-services-using-the-reportviewer-controls"></a>使用 ReportViewer 控件集成 Reporting Services
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] 提供两个 ReportViewer 控件将报表查看功能到应用程序。 一个控件版本针对基于 Windows 窗体的应用程序，另一个版本针对 Web 窗体应用程序。 每个控件都提供类似的功能，但分别设计为针对其各自的环境。 这两个控件都可以处理已部署到报表服务器（远程处理模式）的报表或已复制到尚未安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的计算机（本地处理模式）的报表。  
  
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
  
## <a name="see-also"></a>请参阅  
 [将 Reporting Services 集成到应用程序中](../application-integration/integrating-reporting-services-into-applications.md)   
 [创建 SSRS 报表使用 Visual Studio （专业回答）](http://go.microsoft.com/fwlink/?LinkId=321991)  
  
  
