---
description: SaveOptionsEnum
title: SaveOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
author: rothja
ms.author: jroth
ms.openlocfilehash: 56e16ff6ca93dde78531394dc474a2e5cc817348
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989308"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
指定在从 [流](./stream-object-ado.md) 对象保存时是否应创建或覆盖文件。 这些值可以是 **adSaveCreateNotExist** 或 **adSaveCreateOverWrite**。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|默认。 如果 *FileName* 参数指定的文件尚不存在，则创建一个新文件。|  
|**adSaveCreateOverWrite**|2|如果*Filename*参数指定的文件已存在，则使用当前打开的**流**对象中的数据覆盖该文件。 如果 *Filename* 参数指定的文件不存在，则创建新的文件。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 这些常量没有 ADO/WFC 等效项。  
  
## <a name="applies-to"></a>适用于  
 [SaveToFile 方法](./savetofile-method.md)