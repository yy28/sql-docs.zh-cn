---
title: "STIsEmpty (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIsEmpty_TSQL
- STIsEmpty (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsEmpty method
ms.assetid: 4cbc66e3-9035-4ecf-8f5a-6301f168c26c
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 571a7c66f1472fb18cf9c6bc933bb41ab673de0b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="stisempty-geography-data-type"></a>STIsEmpty（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  如果返回 1 **geography**实例为空。 如果将返回 0 **geography**实例不为空。  
  
## <a name="syntax"></a>语法  
  
```  
  
.STIsEmpty ( )  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**位**  
  
 CLR 返回类型： **SqlBoolean**  
  
## <a name="examples"></a>示例  
 下面的示例创建一个空的 `geography` 实例并使用 `STIsEmpty()` 来验证该实例是否为空。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON EMPTY', 4326);  
SELECT @g.STIsEmpty();  
```  
  
## <a name="see-also"></a>另请参阅  
 [地域实例上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
