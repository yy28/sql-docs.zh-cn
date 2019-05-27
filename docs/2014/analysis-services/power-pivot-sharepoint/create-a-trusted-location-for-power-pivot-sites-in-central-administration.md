---
title: 在管理中心中创建 PowerPivot 站点的受信任的位置 |Microsoft Docs
ms.custom: ''
ms.date: 04/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a666f365-cd93-43a3-9d3d-e429dfc19b66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b54c06d86490c92936d147f2876d663f43d99fac
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071590"
---
# <a name="create-a-trusted-location-for-powerpivot-sites-in-central-administration"></a>Create a trusted location for PowerPivot sites in Central Administration
  通过 Excel Services，您可以指定哪些位置是您在 SharePoint 服务器上打开的工作簿的有效存储库。 这些位置称为“受信任位置”，您可以对您创建的每个受信任位置使用不同的配置设置。 对于部署 PowerPivot for SharePoint 而言，您可以考虑为包含 PowerPivot 工作簿的站点创建一个受信任位置，以便您可以应用最适合进行 PowerPivot 数据访问的设置，同时为场的剩余部分保留默认设置。  
  
  
  
## <a name="prerequisites"></a>先决条件  
 您必须是场或服务管理员才能将某一 URL 指定为受信任位置。  
  
 您必须知道包含 PowerPivot 库或用于存储工作簿的其他库的 SharePoint 站点的 URL 地址。 若要获取的地址，打开包含库的站点，右键单击**PowerPivot 库**，选择**属性**，然后将复制的第一部分的地址 (URL)，其中包含服务器名称和站点路径。  
  
##  <a name="overview"></a> 概述  
 初次安装 Excel Services 时会将“http://”指定为其受信任位置，这意味着可以在服务器上打开场中任何站点上的工作簿。 如果您需要更紧密地控制哪些位置被视为可信的，则可以创建新的受信任位置（这些位置映射到场中的特定站点），然后，改变每个位置的设置和权限。  
  
 如果对于场的其余部分您想要保留默认值，同时应用最适合进行 PowerPivot 数据访问的其他设置，则为承载 PowerPivot 工作簿的站点创建新的受信任位置尤其有用。 例如，针对 PowerPivot 工作簿进行优化的受信任位置可能具有的最大工作簿大小为 50 MB，而场的其他部分使用默认值 10MB。  
  
 如果您正在使用 PowerPivot 库来预览已发布工作簿，并且遇到数据刷新警告而不是所期望的预览图像，则建议创建受信任位置。 PowerPivot 库使用文档内的数据和展示信息呈现报表和工作簿的缩略图。 如果为受信任位置启用了“数据刷新时警告”，则 PowerPivot 库可能没有足够的权限来执行刷新，这会导致出现错误，而不是显示缩略图。 将包含 PowerPivot 库的站点添加为新的受信任位置可以消除此问题。  
  
##  <a name="create"></a> 为 PowerPivot 数据访问创建受信任的位置  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击“Excel Services 服务应用程序”。  
  
3.  单击 **“受信任文件位置”**。  
  
4.  单击 **“添加受信任文件位置”**。  
  
5.  输入包含 PowerPivot 库的站点的 URL。  
  
6.  在“位置类型”中，选择 **Microsoft SharePoint Foundation**。  
  
    > [!IMPORTANT]  
    >  PowerPivot 数据访问不支持 UNC 和 HTTP 位置类型。  
  
7.  接受“会话管理”、“工作簿属性”和“计算行为”中的所有默认属性设置。  
  
8.  在“工作簿属性”中，将 **“工作簿最大大小”** 设置为 **50**。 这会将工作簿文件大小的上限调整到用于文件上载到父 Web 应用程序的上限。 如果您的工作簿大小超过 50 MB，则必须进一步增加该文件大小限制。 有关详细信息，请参阅[配置最大文件上传大小&#40;PowerPivot for SharePoint&#41;](configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。  
  
9. 在“外部数据”中，确认“允许外部数据”设置为 **“受信任的数据连接库和嵌入连接”**。 此设置是工作簿中 PowerPivot 数据访问所必需的。  
  
10. 还在“外部数据”中，对于“刷新时警告”，取消选中 **“启用刷新警告”** 的复选框。 取消选中该复选框将允许 PowerPivot 库跳过例行的警告消息，而显示工作簿的预览图像。  
  
11. 单击“确定” 。  
  
## <a name="see-also"></a>请参阅  
 [PowerPivot 库](../../2014-toc/books-online-for-sql-server-2014.md)   
 [创建和自定义 PowerPivot 库](create-and-customize-power-pivot-gallery.md)   
 [使用 PowerPivot 库](use-power-pivot-gallery.md)  
  
  
