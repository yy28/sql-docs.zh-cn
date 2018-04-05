---
title: 数据库元素 (DTA) 的工作负荷 |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02bf075186f8bc9c8efc6fb05b9288f636494a7c
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="database-element-for-workload-dta"></a>工作负荷的数据库元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]指定工作负荷跟踪表所在的数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Workload>  
  <Database>  
   ...code removed here...  
  </Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|如果未指定其他类型的工作负荷，则必须使用一次。 必须为 **工作负荷**父级指定 **EventString**、 **文件** 或 **数据库** 子元素，但只能使用一种类型。 例如，如果使用 **Database** 元素指定了工作负荷，则不可以在同一 XML 输入文件中使用 **File** 元素指定工作负荷。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[工作负荷元素 &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)|  
|**子元素**|[数据库 &#40; DTA &#41; 的名称元素](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [数据库 &#40; DTA &#41; 的架构元素](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>注释  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **DatabaseDetailsTypecomplexType** 。 请不要将此 **Database** 元素与根级父元素为 **Configuration** 元素的元素相混淆。 （请参阅[用于配置的数据库元素 (DTA)](../../tools/dta/database-element-for-configuration-dta.md)。）  
  
## <a name="example"></a>示例  
 有关使用该 **Database** 元素的示例，请参阅 [工作负荷元素 (DTA)](../../tools/dta/workload-element-dta.md)中的代码示例。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
