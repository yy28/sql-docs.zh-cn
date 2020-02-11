---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a8c4ddb27bbc6831095062af5491fb501b6d5b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933049"
---
# <a name="editmodeenum"></a>EditModeEnum
指定记录的编辑状态。  
  
|一直|值|说明|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|指示没有正在进行的编辑操作。|  
|**adEditInProgress**|1|指示当前记录中的数据已修改但未保存。|  
|**adEditAdd**|2|指示已调用[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法，并且复制缓冲区中的当前记录是尚未保存到数据库中的新记录。|  
|**adEditDelete**|4|指示当前记录已被删除。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|一直|  
|--------------|  
|AdoEnums. EditMode|  
|AdoEnums. EditMode|  
|AdoEnums. EditMode|  
|AdoEnums. EditMode. DELETE|  
  
## <a name="applies-to"></a>应用于  
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)
