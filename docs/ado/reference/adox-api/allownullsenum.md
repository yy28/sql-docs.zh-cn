---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48e9d8c40d2ab76b902d285526fcd9e9abf7be07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967337"
---
# <a name="allownullsenum"></a>AllowNullsEnum
指定要编制索引是否具有 null 值的记录。  
  
|常量|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|索引允许在其中的键列均为 null 的项。 如果在键列中输入 null 值，则该条目插入到索引。|  
|**adIndexNullsDisallow**|1|默认值。 索引不允许在其中的键列均为 null 的项。 如果在键列中输入 null 值，则将会出错。|  
|**adIndexNullsIgnore**|2|索引不会插入包含 null 键的条目。 如果在键列中输入 null 值，则将忽略该条目并不会出现错误。|  
|**adIndexNullsIgnoreAny**|4|索引不会插入其中一些键列具有 null 值的条目。 对于具有多列索引键，如果某个列中，输入 null 值将忽略该条目并不会出现错误。|  
  
## <a name="applies-to"></a>适用范围  
 [IndexNulls 属性 (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
