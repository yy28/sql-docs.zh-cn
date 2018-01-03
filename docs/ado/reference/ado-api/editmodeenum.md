---
title: "EditModeEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: EditModeEnum
helpviewer_keywords: EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d5f1463191ced2f9e4768193ae5c79c5619896a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="editmodeenum"></a>EditModeEnum
指定的记录的编辑状态。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|指示任何编辑操作正在进行。|  
|**adEditInProgress**|@shouldalert|指示当前记录中的数据已修改但尚未保存。|  
|**adEditAdd**|2|指示[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)已调用方法，并且复制缓冲区中的当前记录是一条新记录，不保存到数据库中。|  
|**adEditDelete**|4|指示当前记录已被删除。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>适用范围  
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)
