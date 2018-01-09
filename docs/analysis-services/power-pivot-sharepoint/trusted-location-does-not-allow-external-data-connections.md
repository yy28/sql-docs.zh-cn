---
title: "受信任位置不允许外部数据连接 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: dc0cedfd-a7d0-40ef-bdd6-ea508130640a
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 84dcf4dd95bc3848e6e8f0e66478f8fc99e2b3f2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="trusted-location-does-not-allow-external-data-connections"></a>受信任的位置不允许外部数据连接
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]包含的 Excel 工作簿的[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]数据，Excel Services 返回此错误，如果它无法连接到嵌入的数据源。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Services 配置为拒绝外部数据访问。|  
|消息正文|存储工作簿的受信任位置不允许外部数据连接。 以下连接刷新失败： [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿包含嵌入数据连接。 若要支持通过切片器和筛选器进行的工作簿交互，Excel Services 必须配置为允许通过嵌入连接信息的外部数据访问。 对于检索在场中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器上加载的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据，外部数据访问是必需的。  
  
## <a name="user-action"></a>用户操作  
 更改配置设置以便允许嵌入数据源。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击 **“Excel Services 应用程序”**。  
  
3.  单击 **“受信任文件位置”**。  
  
4.  单击 **http://** 或者要配置的位置。  
  
5.  在“外部数据”的“允许外部数据”中，单击 **“受信任的数据连接库和嵌入连接”**。  
  
6.  单击“确定” 。  
  
 此外，你还可以为包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿的站点创建新的受信任位置，然后仅修改该站点的配置设置。 有关详细信息，请参阅 [在管理中心中为 Power Pivot 站点创建受信任位置](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
  
