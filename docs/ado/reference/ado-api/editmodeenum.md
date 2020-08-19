---
description: EditModeEnum
title: EditModeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
author: rothja
ms.author: jroth
ms.openlocfilehash: 64310c3399d24d557fc0896587dad0dc4fde091b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444039"
---
# <a name="editmodeenum"></a>EditModeEnum
指定记录的编辑状态。  
  
|返回的常量|值|描述|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|指示没有正在进行的编辑操作。|  
|**adEditInProgress**|1|指示当前记录中的数据已修改但未保存。|  
|**adEditAdd**|2|指示已调用 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 方法，并且复制缓冲区中的当前记录是尚未保存到数据库中的新记录。|  
|**adEditDelete**|4|指示当前记录已被删除。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums. EditMode|  
|AdoEnums. EditMode|  
|AdoEnums. EditMode|  
|AdoEnums. EditMode. DELETE|  
  
## <a name="applies-to"></a>适用于  
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)
