---
title: MakeValid（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MakeValid
- MakeValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid (geometry Data Type)
ms.assetid: 38673010-ab77-4ebb-9c4d-b26b79e3b7ea
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cd5a5702ff7ae3580158e574b0c84a7abb74842f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="makevalid-geometry-data-type"></a>MakeValid（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

将无效 **geometry** 实例转换为具有有效开放地理空间信息联盟 (OGC) 类型的 **geometry** 实例。
  
## <a name="syntax"></a>语法  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geometry  
  
 CLR 返回类型：SqlGeometry  
  
## <a name="remarks"></a>Remarks  
 此方法可能会导致 **geometry** 实例的类型有所变化，还会导致 **geometry** 实例的点略微移位。  
  
## <a name="examples"></a>示例  
 第一个示例创建一个与其自身重叠的无效 `LineString` 实例，并使用 `STIsValid()` 来确认该实例是无效实例。 `STIsValid()` 针对无效实例返回值 0。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 0);  
SELECT @g.STIsValid();  
```  
  
 第二个示例使用 `MakeValid()` 使该实例有效并测试该实例是否的确有效。 `STIsValid()` 针对有效实例返回值 1。  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 第三个示例验证是否已将该实例更改为有效实例。  
  
```  
SELECT @g.ToString();  
```  
  
 在此示例中，在选择 `LineString` 实例时，值将作为有效的 `MultiLineString` 实例返回。  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
 下面的示例将 CircularString 实例转换为 Point 实例。  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 1 1, 1 1)';  
SELECT @g.MakeValid().ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [STIsValid（geometry 数据类型）](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [几何图形实例上的扩展方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

