---
title: "在管理中心中创建 Power Pivot 站点的受信任的位置 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a666f365-cd93-43a3-9d3d-e429dfc19b66
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f2913ee3aa26a01a704fbdd94a4d01b7044f73a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-trusted-location-for-power-pivot-sites-in-central-administration"></a>在管理中心中为 Power Pivot 站点创建受信任位置
  通过 Excel Services，您可以指定哪些位置是您在 SharePoint 服务器上打开的工作簿的有效存储库。 这些位置称为“受信任位置”，您可以对您创建的每个受信任位置使用不同的配置设置。 对于部署 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 而言，可以考虑为包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿的站点创建一个受信任位置，以便可以应用最适合进行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据访问的设置，同时为场的剩余部分保留默认设置。  
  
  
## <a name="prerequisites"></a>先决条件  
 您必须是场或服务管理员才能将某一 URL 指定为受信任位置。  
  
 必须知道包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库或用于存储工作簿的其他库的 SharePoint 站点的 URL 地址。 若要获取该地址，请打开包含库的站点，右键单击“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库”，选择“属性”，然后复制包含服务器名称和站点路径的“地址 (URL)”的第一部分。  
  
##  <a name="overview"></a> 概述  
 初次安装 Excel Services 时会将“http://”指定为其受信任位置，这意味着可以在服务器上打开场中任何站点上的工作簿。 如果您需要更紧密地控制哪些位置被视为可信的，则可以创建新的受信任位置（这些位置映射到场中的特定站点），然后，改变每个位置的设置和权限。  
  
 如果想要为场的其余部分保留默认值，同时应用最适合进行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据访问的其他设置，则为承载 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿的站点创建新的受信任位置尤其有用。 例如，针对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿进行优化的受信任位置可能具有的最大工作簿大小为 50 MB，而场的其他部分使用默认值 10 MB。  
  
 如果正在使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库来预览已发布工作簿，并且遇到数据刷新警告而不是所期望的预览图像，则建议创建受信任位置。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库使用文档内的数据和呈现的信息来呈现报表和工作簿的缩略图。 如果为受信任位置启用了“数据刷新时警告”，则 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库可能没有足够的权限来执行刷新，这会导致出现错误，而不是显示缩略图。 将包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库的站点添加为新的受信任位置可以消除此问题。  
  
##  <a name="create"></a> 如何为 Power Pivot 数据访问创建受信任位置  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击“Excel Services 服务应用程序”。  
  
3.  单击 **“受信任文件位置”**。  
  
4.  单击 **“添加受信任文件位置”**。  
  
5.  输入包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库的站点的 URL。  
  
6.  在“位置类型”中，选择 **Microsoft SharePoint Foundation**。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据访问不支持 UNC 和 HTTP 位置类型。  
  
7.  接受“会话管理”、“工作簿属性”和“计算行为”中的所有默认属性设置。  
  
8.  在“工作簿属性”中，将 **“工作簿最大大小”** 设置为 **50**。 这会将工作簿文件大小的上限调整到用于文件上载到父 Web 应用程序的上限。 如果您的工作簿大小超过 50 MB，则必须进一步增加该文件大小限制。 有关详细信息，请参阅[配置最大文件上传大小 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。  
  
9. 在“外部数据”中，确认“允许外部数据”设置为 **“受信任的数据连接库和嵌入连接”**。 此设置是工作簿中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据访问所必需的。  
  
10. 还在“外部数据”中，对于“刷新时警告”，取消选中 **“启用刷新警告”**的复选框。 取消选中该复选框将允许 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库跳过例行的警告消息，而显示工作簿的预览图像。  
  
11. 单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [PowerPivot 库](http://msdn.microsoft.com/library/2a0db616-e08e-4062-aac8-979f8cad7794)   
 [创建和自定义 Power Pivot 库](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)   
 [使用 Power Pivot 库](../../analysis-services/power-pivot-sharepoint/use-power-pivot-gallery.md)  
  
  

