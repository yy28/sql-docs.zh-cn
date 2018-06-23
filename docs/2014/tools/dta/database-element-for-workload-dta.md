---
title: 工作负荷的数据库元素 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6380708319286a984ef54ef3820fab22821047bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018508"
---
# <a name="database-element-for-workload-dta"></a>工作负荷的数据库元素 (DTA)
  指定工作负荷跟踪表所在的数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Workload>  
  <Database>  
   ...code removed here...  
  </Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|如果未指定其他类型的工作负荷，则必须使用一次。 必须指定`EventString`、 `File`，或`Database`子元素`Workload`父，但仅有一个类型使用。 例如，如果使用 `Database` 元素指定了工作负荷，则不可以在同一 XML 输入文件中使用 `File` 元素指定工作负荷。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[工作负荷元素&#40;DTA&#41;](workload-element-dta.md)|  
|**子元素**|[数据库的名称元素&#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [数据库的架构元素&#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **DatabaseDetailsTypecomplexType** 。 请不要将此 `Database` 元素与根级父元素为 `Configuration` 元素的元素相混淆。 （请参阅[用于配置的数据库元素 (DTA)](database-element-for-configuration-dta.md)。）  
  
## <a name="example"></a>示例  
 有关此用法示例`Database`元素，请参阅中的代码示例[工作负荷元素&#40;DTA&#41;](workload-element-dta.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  