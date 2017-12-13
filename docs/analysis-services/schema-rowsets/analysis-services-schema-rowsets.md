---
title: "Analysis Services 架构行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- SSAS, data access interfaces
- Analysis Services data access interfaces, schema rowsets
- data access interfaces [Analysis Services]
- XML for Analysis, schema rowsets
- rowsets [Analysis Services], retrieving schema rowsets
- retrieving schema rowsets
- XMLA, schema rowsets
- rowsets [Analysis Services]
- schema rowsets [Analysis Services], retrieving
ms.assetid: 820d4b59-d428-4616-b792-c848e5da407e
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ed5393a6406aa031f141d6a635f0690983626dd5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="analysis-services-schema-rowsets"></a>Analysis Services 架构行集
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]架构行集是预定义的表包含有关 Analysis Services 对象和服务器状态，包括数据库架构、 活动会话、 连接、 命令和服务器执行的作业的信息。 您可以在 SQL Server Management Studio 的 XML/A 脚本窗口中查询架构行集表、对架构行集运行 DMV 查询，或创建包含架构行集信息的自定义应用程序（例如，检索可用于创建报表的可用维度列表的报表应用程序）。  
  
> [!NOTE]  
>  如果你使用的架构行集在 XML/A 脚本，在中返回的信息*结果*参数[发现](../../analysis-services/xmla/xml-elements-methods-discover.md)方法结构根据本中介绍的行集列布局部分。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持 XML for Analysis 规范所需的行集。 XMLA 访问接口还支持 OLE DB、OLE DB for OLAP 和 OLE DB for Data Mining 数据源提供程序的某些标准架构行集。 下列主题介绍了支持的行集。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[XML for Analysis 架构行集](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)|介绍 XMLA 访问接口支持的 XMLA 行集。|  
|[OLE DB 架构行集](../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)|介绍 XMLA 访问接口支持的 OLE DB 架构行集。|  
|[OLE DB for OLAP 架构行集](../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)|介绍 XMLA 访问接口支持的 OLE DB for OLAP 架构行集。|  
|[数据挖掘架构行集](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)|介绍 XMLA 访问接口支持的数据挖掘架构行集。|  
  
## <a name="see-also"></a>另请参阅  
 [多维模型数据访问 &#40;Analysis Services-多维数据 &#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)   
 [使用动态管理视图 (DMV) 监视 Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
