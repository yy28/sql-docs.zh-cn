---
title: DISCOVER_STORAGE_TABLES 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 13df6f10-8efe-4fe9-83a6-96d108809ed1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2bfa54e95a97aeb8bd79b9551da461473c4be980
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="discoverstoragetables-rowset"></a>DISCOVER_STORAGE_TABLES 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  允许客户端确定在表格或 SharePoint 模式下运行的 Analysis Services 数据库中包括的表。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_STORAGE_TABLES**行集包含以下各列。  
  
|**列名**|**类型指示符**|**长度**|**Description**|  
|---------------------|------------------------|----------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**||指定包含表的数据库名称。<br /><br /> **DISCOVER_STORAGE_TABLES**行集可通过使用此列来限制。 如果未使用此列来限制行集，则使用当前数据库。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||指定包含表的多维数据集或模型。<br /><br /> **DISCOVER_STORAGE_TABLES**行集可通过使用此列来限制。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**||度量值组的名称。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**||分区的名称。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||维度的名称。|  
|**针对 TABLE_ID 所**|**DBTYPE_WSTR**||用于存储表属性的表的 ID。|  
|**TABLE_PARTITIONS_COUNT**|**DBTYPE_ WSTR**||表分区计数。|  
|**HINT_TABLE_TYPE**|**DBTYPE_ WSTR**||表类型的提示。|  
|**ROWS_COUNT**|**DBTYPE_UI4**||在分区中的行数。|  
|**RIVIOLATION_COUNT**|**DBTYPE_UI4**||具有引用完整性冲突的行数。|  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_STORAGE_TABLES**行集可限制在下表中列出的列。  
  
|**列名**|**类型指示符**|**限制状态**|  
|---------------------|------------------------|---------------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|選擇性|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|選擇性|  
  
## <a name="example"></a>示例  
 下面的代码示例从当前连接上的默认数据库返回存储表以及各存储表中的行数的列表。  
  
```  
SELECT TABLE_ID, ROWS_COUNT  
FROM $system.DISCOVER_STORAGE_TABLES  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
