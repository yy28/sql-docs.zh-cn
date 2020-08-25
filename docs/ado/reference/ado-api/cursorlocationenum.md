---
description: CursorLocationEnum
title: CursorLocationEnum |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 950d6310bff0bf27affe70899ba63914c9ae0ec4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775526"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
指定游标服务的位置。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|使用由本地游标库提供的客户端游标。 本地游标服务通常会允许驱动程序提供的游标中的许多功能，因此，使用此设置可能会提供有关将启用的功能的优势。 为了向后兼容，还支持同义词 **adUseClientBatch** 。|  
|**adUseNone**|1|不使用游标服务。  (此常量已过时，只是为了实现向后兼容性而显示。 ) |  
|**adUseServer**|2|默认。 使用由数据提供程序或驱动程序提供的游标。 这些游标有时非常灵活，并允许其他用户对数据源所做的更改进行其他敏感性。 但 [OLE DB 的 Microsoft 游标服务](../../guide/data/the-microsoft-cursor-service-for-ole-db.md)的某些功能，如解除关联<br /><br /> 无法使用服务器端游标模拟[记录集](./recordset-object-ado.md)对象，这些功能在此设置下不可用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums. CursorLocation|  
|AdoEnums. CursorLocation|  
|AdoEnums. CursorLocation. 服务器|  
  
## <a name="applies-to"></a>适用于  
 [CursorLocation 属性 (ADO)](./cursorlocation-property-ado.md)