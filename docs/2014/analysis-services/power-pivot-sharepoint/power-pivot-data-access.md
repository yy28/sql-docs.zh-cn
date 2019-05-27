---
title: PowerPivot 数据访问 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 83dc82da-91fb-4e47-91a8-0e0db67339b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97f5d2045601f72c3536fbf2d4e469eb5eb20fbe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071245"
---
# <a name="powerpivot-data-access"></a>PowerPivot 数据访问
  本主题介绍从发布到 SharePoint 库的 PowerPivot 工作簿检索数据的方法。  
  
 PowerPivot 数据存储于 Excel 工作簿中。 连接字符串是指向 SharePoint 站点上的工作簿的 URL。  
  
 PowerPivot 数据最常由包含它的工作簿用作数据透视表和数据透视图背后蕴含的数据。 此外，PowerPivot 数据也可以用作外部数据源，其中，工作簿、面板或报表连接到 SharePoint 中的单独 Excel (.xlsx) 文件并且检索数据以供以后使用。 通常使用 PowerPivot 数据的客户端工具是 Excel、[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、其他 Reporting Services 报表和 PerformancePoint。  
  
 在桌面上，PowerPivot 外接程序使用 AMO 和 ADOMD.NET 来创建、处理和查询客户端工作区中的 PowerPivot 数据。  
  
 在 SharePoint 场上，Excel Services 使用本地 MSOLAP OLE DB 访问接口来连接到 PowerPivot 数据。 该访问接口向场中的 PowerPivot for SharePoint 服务器发出连接请求。 该服务器将加载数据，运行查询，并且返回结果集。  
  
##  <a name="queryproc"></a> 查询 SharePoint 中的 PowerPivot 数据  
 在查看 SharePoint 库中的 PowerPivot 工作簿时，分别由场内的 Analysis Services 服务器实例来检测、提取和处理该工作簿内的 PowerPivot 数据，同时由 Excel Services 来呈现表示层。 在带有 PowerPivot 外接程序的浏览器窗口或 Excel 2010 桌面应用程序中，您可以查看经过完全处理的工作簿。  
  
 下图说明了场对查询处理请求的处理流程。 由于 PowerPivot 数据是 Excel 2010 工作簿的一部分，因此当用户打开 SharePoint 库中的一个 Excel 工作簿并与包含 PowerPivot 数据的数据透视表或数据透视图进行交互时，就会产生查询处理请求。  
  
 ![GMNI_DataProcReq](../media/gmni-dataprocreq.gif "GMNI_DataProcReq")  
  
 Excel Services 和 PowerPivot for SharePoint 组件处理同一个工作簿 (.xlsx) 文件的不同部分。 Excel Services 检测 PowerPivot 数据，并向场中的 PowerPivot 服务器发出处理请求。 PowerPivot 服务器将该请求分配给 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]实例，该实例从内容库中的工作簿内提取数据并加载数据。 存储在内存中的数据合并回呈现的工作簿中，并传递回 Excel Web Access，以便在浏览器窗口中显示。  
  
 并不是 PowerPivot 工作簿中的所有数据都由 PowerPivot for SharePoint 处理。 Excel Services 处理工作表中的表格和单元格数据。 只有与 PowerPivot 数据对应的数据透视表、数据透视图和切片器才由 PowerPivot for SharePoint 处理。  
  
## <a name="see-also"></a>请参阅  
 [连接到 Analysis Services](../instances/connect-to-analysis-services.md)   
 [表格模型数据访问](../tabular-models/tabular-model-data-access.md)  
  
  
