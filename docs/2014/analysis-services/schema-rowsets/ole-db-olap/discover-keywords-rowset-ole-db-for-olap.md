---
title: DISCOVER_KEYWORDS 行集 (OLE DB for OLAP) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DISCOVER_KEYWORDS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_KEYWORDS rowset
ms.assetid: 70cc680d-9530-469b-8a61-4e6779aec17a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8fb1249cb328aac0e24d74b1ab53a4def09c4646
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130967"
---
# <a name="discoverkeywords-rowset-ole-db-for-olap"></a>DISCOVER_KEYWORDS 行集 (OLE DB for OLAP)
  枚举该访问接口保留的单词列表。  
  
## <a name="rowset-columns"></a>行集列  
 DISCOVER_KEYWORDS 行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`Keyword`|`DBTYPE_WSTR`||保留关键字。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 对于 DISCOVER_KEYWORDS 行集，可对下表中列出的列进行限制。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`Keyword`|`DBTYPE_WSTR`|可选。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  
