---
description: AffectEnum
title: AffectEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
author: rothja
ms.author: jroth
ms.openlocfilehash: 551c2ec7b8351ed17841ed1a4073c1a411dc77d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451289"
---
# <a name="affectenum"></a>AffectEnum
指定哪些记录受操作影响。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|如果没有应用于**记录集**的[筛选器](../../../ado/reference/ado-api/filter-property.md)，则会影响所有记录。<br /><br /> 如果 " **筛选器** " 属性设置为字符串条件 (如 "Author = ' Smith '" ) ，则操作会影响当前章节中的可见记录。<br /><br /> 如果 " **筛选器** " 属性设置为 [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) 或书签数组的成员，则该操作将影响 **记录集**的所有行。 **注意： adAffectAll** 在 Visual Basic 对象浏览器中处于隐藏状态。|  
|**adAffectAllChapters**|4|影响 **记录集**的所有同级章节中的所有记录，包括那些通过当前应用的任何 **筛选器** 看不到的记录。|  
|**adAffectCurrent**|1|仅影响当前记录。|  
|**adAffectGroup**|2|仅影响满足当前 [Filter](../../../ado/reference/ado-api/filter-property.md) 属性设置的记录。 若要使用此选项，必须将 **Filter** 属性设置为 **FilterGroupEnum** 值或 **书签** 的数组。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums。所有|  
|AdoEnums. ALLCHAPTERS|  
|AdoEnums 影响。当前|  
|AdoEnums。影响组|  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)  
        [Delete 方法（ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)  
    :::column-end:::
    :::column:::
        [重新同步方法](../../../ado/reference/ado-api/resync-method.md)  
        [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)  
    :::column-end:::
:::row-end:::
