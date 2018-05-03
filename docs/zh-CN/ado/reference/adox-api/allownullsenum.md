---
title: AllowNullsEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b321045efcf77e3e0a5922638b8437903a69bef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="allownullsenum"></a>AllowNullsEnum
指定是否具有 null 值的记录编制索引。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|索引允许在其中的键列都为 null 的项。 如果在键列中输入 null 值，则将条目插入到索引。|  
|**adIndexNullsDisallow**|1|默认值。 索引不允许在其中的键列都为 null 的项。 如果在键列中输入 null 值，将发生错误。|  
|**adIndexNullsIgnore**|2|索引不会插入包含空键的项。 在键列中输入 null 值，如果条目被忽略，且不发生错误。|  
|**adIndexNullsIgnoreAny**|4|索引不会插入其中某些键列具有 null 值的条目。 对于具有多列索引条目被忽略密钥，如果某个列中，输入 null 值，且不发生错误。|  
  
## <a name="applies-to"></a>适用范围  
 [IndexNulls 属性 (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
