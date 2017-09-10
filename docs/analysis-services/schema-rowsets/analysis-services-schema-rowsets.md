---
title: "Analysis Services 架构行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 21cafe5519f9e657a95578aeccbc5773f8eaee97
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-schema-rowsets"></a>Analysis Services 架构行集
  架构行集是预定义的表，其中包含有关 Analysis Services 对象和服务器状态（包括在服务器上执行的数据库架构、活动的会话、连接、命令和作业）的信息。 您可以在 SQL Server Management Studio 的 XML/A 脚本窗口中查询架构行集表、对架构行集运行 DMV 查询，或创建包含架构行集信息的自定义应用程序（例如，检索可用于创建报表的可用维度列表的报表应用程序）。  
  
> [!NOTE]  
>  如果你使用的架构行集在 XML/A 脚本，在中返回的信息*结果*参数[发现](../../analysis-services/xmla/xml-elements-methods-discover.md)方法结构根据本中介绍的行集列布局部分。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持 XML for Analysis 规范所需的行集。 XMLA 访问接口还支持 OLE DB、OLE DB for OLAP 和 OLE DB for Data Mining 数据源提供程序的某些标准架构行集。 下列主题介绍了支持的行集。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[XML for Analysis 架构行集](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)|介绍 XMLA 访问接口支持的 XMLA 行集。|  
|[OLE DB 架构行集合](../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)|介绍 XMLA 访问接口支持的 OLE DB 架构行集。|  
|[OLE DB for OLAP 架构行集](../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)|介绍 XMLA 访问接口支持的 OLE DB for OLAP 架构行集。|  
|[数据挖掘架构行集](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)|介绍 XMLA 访问接口支持的数据挖掘架构行集。|  
  
## <a name="see-also"></a>另请参阅  
 [多维模型数据访问 &#40;Analysis Services-多维数据 &#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)   
 [使用动态管理视图 (DMV) 监视 Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
