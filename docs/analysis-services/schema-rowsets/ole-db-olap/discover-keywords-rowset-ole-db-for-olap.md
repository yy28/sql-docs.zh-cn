---
title: DISCOVER_KEYWORDS 行集 (OLE DB olap) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d4ba6c7ee41c8018af30635d7d28d1e7871f81b9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="discoverkeywords-rowset-ole-db-for-olap"></a>DISCOVER_KEYWORDS 行集 (OLE DB for OLAP)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  枚举该访问接口保留的单词列表。  
  
## <a name="rowset-columns"></a>行集列  
 DISCOVER_KEYWORDS 行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**关键字**|**DBTYPE_WSTR**||保留关键字。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 对于 DISCOVER_KEYWORDS 行集，可对下表中列出的列进行限制。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**关键字**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
