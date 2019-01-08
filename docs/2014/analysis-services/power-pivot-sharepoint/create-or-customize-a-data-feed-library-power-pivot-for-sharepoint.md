---
title: 创建或自定义数据馈送的库 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data feed library
- data feeds [Analysis Services with SharePoint]
ms.assetid: 699fbeb9-42ab-436b-beba-214db51ea3dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3586379cbd22dee4e288a032a9dd850355b2b674
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543555"
---
# <a name="create-or-customize-a-data-feed-library-powerpivot-for-sharepoint"></a>创建或自定义数据馈送库 (PowerPivot for SharePoint)
  *数据馈送库* 是一种特殊用途的 SharePoint 库，允许注册和共享 Atom 数据服务文档 (.atomsvc)。 这些文档向 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿或支持 Atom 数据馈送格式的其他客户端应用程序提供 XML 数据馈送。 数据馈送库与其他 SharePoint 库不同，因为它使你能够：  
  
-   创建或编辑“数据服务文档” ，用于指定与特定馈送的 HTTP 连接。  
  
-   在一个中心位置共享和管理数据服务文档。  
  
-   通过图标直观地标识数据服务文档，以便你可以轻松地从同一库中存储的其他文档中区分出服务文档：![GMNI_IconDataFeed](../media/gmni-icondatafeed.gif "GMNI_IconDataFeed")  
  
 数据馈送库始终包含数据服务文档 (.atomsvc) 文件，并且永远不会包含数据馈送本身。 与由静态 XML 数据构成的数据馈送不同，数据服务文档指定根据请求生成馈送的服务或应用程序的 URL，并且为可重复的导入操作提供可重复使用的连接信息。  
  
 本主题包含以下各节：  
  
 [先决条件](#prereq)  
  
 [创建新的数据馈送库](#createlib)  
  
 [向任何库添加数据馈送内容类型](#addtolib)  
  
##  <a name="prereq"></a> 先决条件  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能集成。 如果数据源库模板类型不可用，最可能的原因就是未满足此先决条件。 有关详细信息，请参阅[针对在管理中心网站集激活 PowerPivot 功能集成](activate-power-pivot-integration-for-site-collections-in-ca.md)。  
  
 您必须是网站所有者才能创建该库。  
  
##  <a name="createlib"></a> 创建新的数据馈送库  
 创建数据馈送库是为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿实现数据馈送的第一步。 因为数据馈送库为数据服务文档提供应用程序和管理页，所以，您必须首先具有此库后，才能创建新文档。  
  
 数据馈送库基于内置模板和预先配置的“数据服务文档内容类型”，该类型定义数据服务文档的属性和行为。  
  
1.  单击该页左上角的 **“网站操作”** 。  
  
2.  单击**更多选项**...  
  
3.  在“库”下，单击 **“数据馈送库”**。  
  
4.  键入名称、说明、启动和版本首选项。 包含说明性信息，以帮助用户将此库识别为用于数据服务文档的存储。  
  
5.  单击 **“创建”**。  
  
 当前网站的导航“快速启动”窗格中将显示指向数据馈送库的链接。  
  
 创建库以后，可以使用它来创建数据服务文档。 有关详细信息，请参阅[使用数据馈送&#40;PowerPivot for SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md)。  
  
##  <a name="addtolib"></a> 向任何库添加数据馈送内容类型  
 如果您不想创建专用的数据馈送库，但仍想要创建和管理 SharePoint 网站中的数据服务文档，则可为将用于共享数据服务文档 (.atomsvc) 文件的任何库手动添加和配置数据服务文档内容类型。  
  
 您必须至少具有“管理列表”权限才能添加和配置内容类型。 此权限是“设计”权限级别和更高级别中所固有的。  
  
 对于要在其中创建或编辑数据馈送注册文档的每个库，都重复以下步骤。  
  
#### <a name="step-1-enable-content-type-management"></a>步骤 1：启用内容类型管理  
  
1.  打开要为其启用多种内容类型的文档库。  
  
2.  在 SharePoint 功能区的“库工具”中，单击 **“库”**。  
  
3.  单击 **“设置”**。  
  
4.  单击 **“库设置”**。  
  
5.  在“常规设置”中，单击 **“高级设置”**。  
  
6.  在“内容类型”的“允许内容类型的管理?”部分中， 单击 **“是”**。  
  
7.  单击“确定” 。  
  
#### <a name="step-2-add-the-data-service-document-content-type"></a>步骤 2：添加数据服务文档内容类型  
  
1.  在“内容类型”部分中，单击 **“从现有网站内容类型添加”**。 如果您看不到此页，则返回网站，在“库工具”中单击 **“库”** ，然后单击 **“库设置”**。  
  
2.  在“内容类型”中，单击 **“从现有网站内容类型添加”**。  
  
3.  在“从以下列表中选择网站内容类型:”中，选择 **“商业智能”**。  
  
4.  在“可用网站内容类型”中，单击 **“数据服务文档”**，然后单击 **“添加”** 将所选内容类型移至“要添加的内容类型”列表中。  
  
5.  单击“确定” 。  
  
#### <a name="step-3-verify-data-service-document-configuration"></a>步骤 3：验证数据服务文档配置  
  
1.  打开网站主页。  
  
2.  打开库。  
  
3.  在 SharePoint 功能区上，单击 **“文档”**。  
  
4.  在“新建文档”上单击向下箭头，然后选择 **“数据服务文档”**。 此时应该显示“新建数据服务文档”页。  
  
## <a name="see-also"></a>请参阅  
 [使用数据馈送&#40;PowerPivot for SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md)   
 [删除 PowerPivot 数据馈送的库](delete-a-power-pivot-data-feed-library.md)   
 [在管理中心的 PowerPivot 服务器管理和配置](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [PowerPivot 数据馈送](power-pivot-data-feeds.md)  
  
  
