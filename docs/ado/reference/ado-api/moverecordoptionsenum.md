---
title: MoveRecordOptionsEnum |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 849f3720d831c17b6b9d6d2829ae0b28f19992de
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762438"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
指定[Record](../../../ado/reference/ado-api/record-object-ado.md) object [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法的行为。  
  
|返回的常量|值|说明|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|默认。 执行默认移动操作：如果目标文件或目录已存在，操作将失败，并且操作将更新超文本链接。|  
|**adMoveOverWrite**|1|覆盖目标文件或目录（即使它已存在）。|  
|**adMoveDontUpdateLinks**|2|通过不更新源**记录**的超文本链接来修改**MoveRecord**方法的默认行为。 默认行为取决于提供程序的功能。 如果提供程序支持，则移动操作更新链接。 如果提供程序无法修复链接或未指定此值，则即使未修复链接，移动也会成功。|  
|**adMoveAllowEmulation**|4|请求提供程序尝试模拟移动（使用下载、上传和删除操作）。 如果由于目标 URL 在不同的服务器上或由不同于源的提供程序服务而导致移动**记录**的尝试失败，这可能会导致延迟或数据丢失，原因是在提供程序之间移动资源时有不同的提供程序功能。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>应用于  
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
