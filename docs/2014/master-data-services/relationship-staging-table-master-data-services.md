---
title: 关系临时表 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 529d0521c320ff2e893a2269fe020d191a6ce284
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960687"
---
# <a name="relationship-staging-table-master-data-services"></a>关系临时表 (Master Data Services)
  使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中的关系临时表 (stg.name_Relationship) 基于成员之间的相互关系更改显式层次结构中的成员位置。  
  
##  <a name="table-columns"></a><a name="TableColumns"></a>表列  
 下表说明 Relationship 临时表中每个字段的用途。  
  
|列名|说明|  
|-----------------|-----------------|  
|**ID**|自动分配的标识符。 不要在此字段中输入值。 如果尚未处理此批次，则此字段为空。|  
|**RelationshipType**<br /><br /> 必需|正在设置的关系的类型。 可能的值包括：<br /><br /> **1**：父级<br /><br /> **2**：同级（同一级）|  
|**ImportStatus_ID**<br /><br /> 必需|导入过程的状态。 可能的值包括：<br /><br /> **0**- 指定此值表示记录已经准备好临时存储。<br /><br /> **1**- 自动分配的值，表示记录的暂存过程已成功。<br /><br /> **2**- 自动分配的值，表示记录的临时过程已失败。|  
|**Batch_ID**<br /><br /> 仅对 Web 服务为必需的|自动分配的标识符，该标识符将记录分组以便临时存储。 将为此批次中的所有成员分配此标识符，此标识符显示在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 用户界面中的 **ID** 列。<br /><br /> 如果尚未处理此批次，则此字段为空。|  
|**BatchTag**<br /><br /> 必需，但是 Web 服务除外|批次的唯一名称，最多包含 50 个字符。|  
|**HierarchyName**<br /><br /> 必需|显式层次结构名称。 每个合并成员只能属于一个层次结构。|  
|**ParentCode**<br /><br /> 必需|对于父-子关系，是将为子叶成员或合并成员的父级的合并成员代码。<br /><br /> 对于同级关系，为以下同级之一的代码。|  
|**ChildCode**<br /><br /> 必需|对于父-子关系，是将为子级的合并成员或叶成员的代码。<br /><br /> 对于同级关系，为以下同级之一的代码。|  
|**排序顺序**<br /><br /> 可选|一个整数，表示该成员相对于父级下其他成员的成员顺序。 每个子成员应具有唯一标识符。|  
|**ErrorCode**|显示错误代码。 有关 **ImportStatus_ID** 为 **2**的所有记录，请参阅 [临时过程错误 (Master Data Services)](staging-process-errors-master-data-services.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 &#40;Master Data Services 的临时过程移动显式层次结构成员&#41;](add-update-and-delete-data-master-data-services.md)   
 [数据导入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [查看临时过程中发生的错误 &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [临时过程错误 (Master Data Services)](staging-process-errors-master-data-services.md)  
  
  
