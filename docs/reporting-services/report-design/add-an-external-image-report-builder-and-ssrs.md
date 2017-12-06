---
title: "添加外部图像（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 7b27b9c57ac19450d279735945bd3d9fe2ea40a7
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>添加外部图像（报表生成器和 SSRS）
  外部图像可在本机模式或 SharePoint 集成模式下处于报表服务器上，或者可处于任何其他网站上。 当您在报表中包括外部图像时，必须验证图像是否存在以及报表读取器是否拥有访问图像的权限。 有关详细信息，请参阅[图像（报表生成器和 SSRS）](../../reporting-services/report-design/images-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>添加外部图像  
  
1.  在报表设计视图的 **“插入”** 选项卡上，单击 **“图像”**。  
  
2.  在设计图面上，单击某个位置，然后拖动一个框调整到所需图像大小。  
  
3.  在 **“图像属性”** 对话框的 **“常规”** 选项卡中，在 **“名称”** 文本框中键入名称，或接受默认名称。  
  
4.  （可选）在“工具提示”文本框中，键入当用户将鼠标指针悬停在以 HTML 格式呈现的报表中的图像上时所要显示的文本。  
  
5.  在 **“选择图像源”**中，选择 **“外部”**。  
  
     对于在本机模式下的报表服务器上的图像，在“使用此图像”框中键入图像的相对路径，例如 ../images/image1.jpg。  
  
     对于 SharePoint 集成模式下报表服务器上的图像，或者任何其他网站上的图像，在“使用此图像”框中键入图像的完整 URL，例如 http://\<SharePointservername>/\<site>/Documents/images/image1.jpg。  
  
     有关详细信息，请参阅[指定外部项的路径（报表生成器和 SSRS）](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
6.  （可选）单击“大小”、“可见性”、“操作”或“边框”以设置图像报表项的其他属性。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [在报表中嵌入图像（报表生成器和 SSRS）](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [添加背景图像（报表生成器和 SSRS）](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md)   
 [“图像属性”对话框 ->“常规”（报表生成器和 SSRS）](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
