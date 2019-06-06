---
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 43c2043917d6b21293fea71566dfdf1202b6f59e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695661"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
指定游标服务的位置。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|使用本地游标库通过提供客户端游标。 局部游标服务通常将允许驱动程序提供的游标不是，可能的许多功能，因此使用此设置可能会提供将启用的功能方面的优势。 为了向后兼容，同义词**adUseClientBatch**也受支持。|  
|**adUseNone**|1|不使用游标服务。 （此常量已过时，将显示仅为了向后兼容性。）|  
|**adUseServer**|2|默认值。 使用由数据访问接口或驱动程序提供的游标。 这些游标时有时非常灵活，并允许其他敏感度对数据源的其他人做的更改。 但是，某些功能[OLE DB 的 Microsoft 游标服务](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)，例如解除关联<br /><br /> [记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，不能模拟与服务器端游标的游标和这些功能会在使用此设置不可用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>适用范围  
 [CursorLocation 属性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
