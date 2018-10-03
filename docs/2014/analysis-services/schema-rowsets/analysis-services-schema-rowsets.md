---
title: Analysis Services 架构行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 474de14a40b24fe113cebf1c933f7e28a351d5bd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227897"
---
# <a name="analysis-services-schema-rowsets"></a>Analysis Services 架构行集
  架构行集是预定义的表，其中包含有关 Analysis Services 对象和服务器状态（包括在服务器上执行的数据库架构、活动的会话、连接、命令和作业）的信息。 您可以在 SQL Server Management Studio 的 XML/A 脚本窗口中查询架构行集表、对架构行集运行 DMV 查询，或创建包含架构行集信息的自定义应用程序（例如，检索可用于创建报表的可用维度列表的报表应用程序）。  
  
> [!NOTE]  
>  如果使用架构行集在 XML/A 脚本，在返回的信息*结果*的参数[Discover](../xmla/xml-elements-methods-discover.md)方法根据在此介绍的行集列布局进行构建部分。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis (XMLA) 访问接口支持 XML for Analysis 规范所需的行集。 XMLA 访问接口还支持 OLE DB、OLE DB for OLAP 和 OLE DB for Data Mining 数据源提供程序的某些标准架构行集。 下列主题介绍了支持的行集。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[XML for Analysis 架构行集](xml/xml-for-analysis-schema-rowsets.md)|介绍 XMLA 访问接口支持的 XMLA 行集。|  
|[OLE DB 架构行集](ole-db/ole-db-schema-rowsets.md)|介绍 XMLA 访问接口支持的 OLE DB 架构行集。|  
|[OLE DB for OLAP 架构行集](ole-db-olap/ole-db-for-olap-schema-rowsets.md)|介绍 XMLA 访问接口支持的 OLE DB for OLAP 架构行集。|  
|[数据挖掘架构行集](data-mining/data-mining-schema-rowsets.md)|介绍 XMLA 访问接口支持的数据挖掘架构行集。|  
  
## <a name="see-also"></a>请参阅  
 [多维模型数据访问&#40;Analysis Services-多维数据&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)   
 [使用动态管理视图&#40;Dmv&#41;若要监视 Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
