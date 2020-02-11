---
title: 工作簿中的数据连接路径指向本地驱动器上的文件或者是无效的 URI。 以下连接无法刷新： PowerPivot 数据 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: bd22e41a-0931-4d32-888a-633a3046fc5e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cc18a2c7111c71b62f77f5f52727a4a50a661ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071038"
---
# <a name="the-data-connection-path-in-the-workbook-points-to-a-file-on-the-local-drive-or-is-an-invalid-uri-the-following-connections-failed-to-refresh-powerpivot-data"></a>工作簿中的数据连接路径指向本地驱动器上的文件或者是无效的 URI。 以下连接无法刷新：PowerPivot 数据
  对于包含 PowerPivot 数据的 Excel 工作簿，如果 Excel Services 无法连接到嵌入数据源，则会返回此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|PowerPivot for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Excel Services 配置为只允许从处于受信任数据连接库中的 .odc 文件的数据连接。|  
|消息正文|工作簿中的数据连接路径指向本地驱动器上的文件或者是无效的 URI。 以下连接无法刷新：PowerPivot 数据|  
  
## <a name="explanation"></a>说明  
 PowerPivot 工作簿包含嵌入数据连接。 若要支持通过切片器和筛选器进行的工作簿交互，Excel Services 必须配置为允许通过嵌入连接信息的外部数据访问。 对于检索在场中 PowerPivot 服务器上加载的 PowerPivot 数据，外部数据访问是必需的。  
  
## <a name="user-action"></a>用户操作  
 更改配置设置以便允许嵌入数据源连接。  
  
1.  在管理中心的 "应用程序管理" 中，单击 "**管理服务应用程序**"。  
  
2.  单击 **“Excel Services 应用程序”**。  
  
3.  单击 **“受信任文件位置”**。  
  
4.  单击 **http://** 或者要配置的位置。  
  
5.  在“外部数据”的“允许外部数据”中，单击 **“受信任的数据连接库和嵌入连接”**。  
  
6.  单击“确定”。   
  
 此外，您还可以为包含 PowerPivot 工作簿的站点创建新的受信任位置，然后仅修改该站点的配置设置。 有关详细信息，请参阅 [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
  
