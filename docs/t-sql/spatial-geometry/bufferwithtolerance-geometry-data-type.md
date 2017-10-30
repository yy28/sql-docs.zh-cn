---
title: "BufferWithTolerance (geometry 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ffa8a350cb4531f9d4a6d1439a4dad0682189266
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance（geometry 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回表示所有点的联合的几何对象值从其距离**几何图形**实例小于或等于指定的值，从而使指定容差。
  
## <a name="syntax"></a>语法  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>参数  
 *距离*  
 是**float**表达式指定的距离**几何图形**围绕其计算的缓冲区的实例。  
  
 *容差*  
 是**float**表达式指定的缓冲区距离的容差。  
  
 *容差*引用中返回的线性近似的理想的缓冲区距离的最大变体。  
  
 例如，点的理想缓冲区距离为圆圈，但是这必须与多边形近似。 公差越小，多边形具有的点就越多，这将增加结果的复杂度，但可减少错误。  
  
 *相对*  
 是**位**指定是否*容差*值是相对或绝对。 如果 'TRUE' 或 1，然后容差是相对的。 而作为计算的产品*容差*参数和直径的实例的边界框。 如果 'FALSE' 或 0，容差是绝对和*容差*值是绝对的最大变体中返回的线性近似的理想的缓冲区距离。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型：**几何图形**  
  
 CLR 返回类型： **SqlGeometry**  
  
## <a name="exceptions"></a>异常  
 *容差*参数必须是大于零。 如果*容差*< = 0 则`System.ArgumentOutOfRangeException`引发。  
  
> [!NOTE]  
>  由于*容差*是**float**类型，`System.Runtime.InteropServices.COMException`容差的给定值是否很小，因舍入的浮点类型问题可能会引发。  
  
## <a name="remarks"></a>注释  
 当*距离*> 0，则请**多边形**或**MultiPolygon**返回实例。  
  
> [!NOTE]  
>  由于距离是**float**，可以相当极小的值为零的计算中。 在这种情况，调用一份**几何图形**返回实例。 请参阅[float 和 real &#40;Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 当*距离*= 0，则调用一份**几何图形**返回实例。  
  
 当*距离*< 0 然后  
  
-   一个空**GeometryCollection**时实例的维度是 0 或 1，则返回实例。  
  
-   当实例维度为 2 或更大时，将返回负缓冲区。  
  
    > [!NOTE]  
    >  负缓冲区还可以创建一个空**GeometryCollection**实例。  
  
 负缓冲区中删除的边界的给定距离内的所有点**几何图形**实例。  
  
 Theorectical 和计算的缓冲区之间的错误是最大 (容差，范围\*1.E 7) 容差所在的值*容差*参数。 有关扩展盘区的详细信息，请参阅[geometry 数据类型方法引用](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)。  
  
## <a name="examples"></a>示例  
 下面的示例创建 `Point` 实例，并使用 `BufferWithTolerance()` 获取环绕该实例的大致缓冲区。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [STBuffer &#40; geometry 数据类型 &#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [在几何图形实例的扩展的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


