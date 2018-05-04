---
title: CursorLocationEnum |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c11977f3ca3ce90efb01ed96ec9075103cdad34d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
指定游标服务的位置。  
  
|常量|“值”|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|使用由局部游标库提供的客户端游标。 局部游标服务通常将允许驱动程序提供的游标不，可能的许多功能，因此使用此设置可能会提供将启用的功能方面的一个优点。 为了向后兼容，同义词**adUseClientBatch**也支持。|  
|**adUseNone**|1|不使用游标服务。 （此常量已过时，并显示只是为了向后兼容性。）|  
|**adUseServer**|2|默认值。 使用由数据提供程序或驱动程序提供的游标。 这些游标有时是非常灵活，并允许其他人对数据源进行的更改具有额外的敏感度。 但是，某些功能的[用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)，例如解除关联<br /><br /> [记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，不能模拟与服务器端游标和这些功能都将使用此设置不可用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>适用范围  
 [CursorLocation 属性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
