---
title: MoveRecordOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MoveRecordOptionsEnum
helpviewer_keywords:
- MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb86b01a42a097210801fd3654ff2af80df24e39
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242451"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
指定的行为[记录](../../../ado/reference/ado-api/record-object-ado.md)对象[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|默认值。 执行默认移动操作：如果目标文件或目录已存在，并且该操作将更新超文本链接，该操作将失败。|  
|**adMoveOverWrite**|1|将覆盖目标文件或目录，即使它已存在。|  
|**adMoveDontUpdateLinks**|2|修改的默认行为**MoveRecord**方法通过不更新源的超文本链接**记录**。 默认行为取决于提供程序的功能。 如果该提供程序是支持移动操作更新这些链接。 如果提供程序不能解决问题的链接，或者如果未指定此值，移动成功甚至当链接具有未得到解决。|  
|**adMoveAllowEmulation**|4|请求的提供程序尝试模拟移动 （使用下载上, 传和删除操作）。 如果尝试将移动**记录**会失败，因为目标 URL 是在不同服务器或服务的一个不同于源访问接口，这可能会导致更高的延迟或数据丢失，由于不同的提供程序功能时提供程序之间移动资源。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量不具有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用范围  
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
