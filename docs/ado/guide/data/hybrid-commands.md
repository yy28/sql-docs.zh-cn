---
description: 混合命令
title: 混合命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- hybrid commands [ADO]
- data shaping [ADO], hybrid commands
ms.assetid: e8ca40e8-459c-40e2-8dd3-3ec6d5ee7b51
author: rothja
ms.author: jroth
ms.openlocfilehash: ec23a74b26be84684965c8e81fffbfd827a9981a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980508"
---
# <a name="hybrid-commands"></a>混合命令
混合命令是部分参数化命令。 例如：  
  
```  
SHAPE {select * from plants}   
   APPEND( {select * from customers where country = ?}   
           RELATE PlantCountry TO PARAMETER 0,   
             PlantRegion TO CustomerRegion )   
```  
  
 混合命令的缓存行为与常规参数化命令的行为相同。  
  
## <a name="see-also"></a>另请参阅  
 [数据定形示例](./data-shaping-example.md)   
 [正式形状语法](./formal-shape-grammar.md)   
 [常用 Shape 命令](./shape-commands-in-general.md)