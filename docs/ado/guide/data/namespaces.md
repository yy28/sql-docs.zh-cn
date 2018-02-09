---
title: "命名空间 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c34bb680f7a066eeb694cf62fba39cabb0d4cbea
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="namespaces"></a>命名空间
ADO 中的 XML 持久性格式使用以下四个命名空间。  
  
## <a name="remarks"></a>注释  
 ADO 中的 XML 持久性格式使用以下四个命名空间。  
  
|Prefix|Description|  
|------------|-----------------|  
|s|表示"XML 数据"命名空间包含的元素和属性定义当前记录集的架构。|  
|dt|引用数据类型定义规范。|  
|rs|引用命名空间包含元素和属性特定于 ADO 记录集属性和属性。|  
|z|引用的当前行集架构。|  
  
 客户端不应将其自己的标记添加到这些命名空间，，如规范所定义。 例如，客户端不应定义为一个命名空间"urn： 架构-microsoft-com:rowset"然后写出类似"rs: MyOwnTag。" 若要了解有关命名空间的详细信息，请参阅[XML 建议中的 W3C 命名空间](http://www.w3.org/TR/REC-xml-names/)。  
  
> [!IMPORTANT]
>  架构标记的 ID 必须是"RowsetSchema，"和用来引用当前行集的架构的命名空间必须指向"#RowsetSchema。"  
  
 请注意，命名空间的前缀 — 冒号和等号之间的部分 — 是任意的。  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 用户可以定义为任何名称，只要整个 XML 文档一致地使用此名称。 ADO 始终写出"s、"rs、"dt，"并"z，"但这些前缀名称不是硬编码到加载组件。  
  
## <a name="see-also"></a>另请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
