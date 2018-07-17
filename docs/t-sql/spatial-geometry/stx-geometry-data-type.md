---
title: STX（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STX (geometry Data Type)
- STX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STX (geometry Data Type)
ms.assetid: 2aef77e8-0460-43f9-bad6-2aae6d8c36f9
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ea60448c5426f0acd21ab58c4fbc6231cdeae1c5
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36247119"
---
# <a name="stx-geometry-data-type"></a>STX（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**Point** 实例的 X 坐标属性。
  
## <a name="syntax"></a>语法  
  
```  
  
.STX  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型：float  
  
 CLR 类型：SqlDouble  
  
## <a name="remarks"></a>Remarks  
 如果 **geometry** 实例不是一个点，此属性的值将为 null。  
  
 该属性为只读。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个 `Point` 实例，并使用 `STX` 检索该实例的 X 坐标。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 8)', 0);  
SELECT @g.STX;  
```  
  
## <a name="see-also"></a>另请参阅  
 [STY（geometry 数据类型）](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [STSrid（geometry 数据类型）](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)   
 [几何图形实例上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

