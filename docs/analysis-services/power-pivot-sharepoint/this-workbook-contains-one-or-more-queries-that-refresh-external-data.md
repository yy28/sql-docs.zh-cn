---
title: "此工作簿包含一个或多个刷新外部数据的查询 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: aa65c992-eb41-4032-9e11-a9ba871b6a3c
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f400a5513fcd16ea5344157e451d06b8fe103796
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="this-workbook-contains-one-or-more-queries-that-refresh-external-data"></a>此工作簿包含一个或多个刷新外部数据的查询
  对于包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的 Excel 工作簿，如果 Excel Services 检测到连接信息，则将显示此警告，并提示你为此工作簿启用或禁用查询。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11_md](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)]|  
|原因|Excel Services 配置为对数据刷新显示警告。|  
|消息正文|此工作簿包含一个或多个用于刷新外部数据的查询。 恶意用户可能设计一个查询来访问机密信息，并将其分发给其他用户或执行其他有害操作。<br /><br /> 如果您信任此工作簿的源，则单击“是”以启用对此工作簿中外部数据的查询。 如果您不确定，则单击“否”，以便不将更改应用到您的工作簿。<br /><br /> 是否要启用对此工作簿中外部数据的查询？|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 工作簿包含由 Excel 使用的嵌入数据连接字符串，以便与加载和计算数据的外部 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务器进行通信。 当启用数据刷新警告时，Excel Services 检测此连接字符串，并相应向用户发出警告。  
  
 若要筛选工作簿中的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 数据并对其执行切片，必须启用查询。 确保你只对你信任的这些 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 工作簿启用查询。  
  
## <a name="user-action"></a>用户操作  
 单击 **“是”** 以启用查询。  
  
 还可以更改配置设置，以便不再发生刷新时警告：  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击 **“Excel Services 应用程序”**。  
  
3.  单击 **“受信任文件位置”**。  
  
4.  单击 **http://** 或者要配置的位置。  
  
5.  在“外部数据”中，取消选中 **“数据刷新时警告”**复选框。  
  
6.  单击 **“确定”**。  
  
 此外，你还可以为包含 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 工作簿的站点创建新的受信任位置，然后仅修改该站点的配置设置。 有关详细信息，请参阅 [Create a trusted location for Power Pivot sites in Central Administration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
  
