---
description: EditModeEnum
title: EditModeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 7e10479aca06eab4a7aa5215f0016dd1f82eab1c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973848"
---
# <a name="editmodeenum"></a>EditModeEnum
指定记录的编辑状态。  
  
|返回的常量|Value|说明|  
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
