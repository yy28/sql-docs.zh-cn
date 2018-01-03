---
title: "IsValidDetailed (geography 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsValidDetailed_TSQL
- IsValidDetailed
dev_langs: TSQL
helpviewer_keywords: IsValidDetailed geography
ms.assetid: f5f0b753-c825-43ce-987d-98655d8d8702
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 80f1b3bc5fa9684a87fbf330f50aca4f3e85aea5
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="isvaliddetailed-geography-data-type"></a>IsValidDetailed（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  返回一条消息，该消息帮助您确定空间对象无效的问题。 当该对象无效时，只返回第一个错误。 当该对象有效时，则返回值 24400。  
  
## <a name="syntax"></a>语法  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回类型： **nvarchar (max)**  
  
 CLR 返回类型：**字符串**  
  
## <a name="remarks"></a>Remarks  
 下表包含可能的返回值：  
  
|返回值|Description|  
|------------------|-----------------|  
|24400|有效|  
|24401|无效，原因未知。|  
|24402|因为点 {0} 是孤立点，这在此类型的对象中是无效的，所以无效。|  
|24403|因为某一对的多边形边重叠，所以无效。|  
|24404|因为多边形环 {0} 与自己或某个其他环相交，所以无效。|  
|24405|因为某个多边形环与自己或某个其他环相交，所以无效。|  
|24406|因为曲线 {0} 退化到点，所以无效。|  
|24407|因为多边形环 {0} 将折叠为点 {1} 一行不有效。|  
|24408|因为多边形环 {0} 未闭合，所以无效。|  
|24409|因为多边形环 {0} 的某个部分处于某个多边形的内部，所以无效。|  
|24410|因为环 {0} 是某个多边形的第一个环、但它不是该多边形的外环，所以无效。|  
|24411|因为环 {0} 位于其多边形的外环 {1} 之外不有效。|  
|24412|不因为具有环 {0} 和 {1} 多边形的内部未连接有效。|  
|24413|因为曲线 {0} 中存在两条重叠的边，所以无效。|  
|24414|因为曲线 {0} 的边重叠 1 曲线 \} 的边不有效。|  
|24415|因为某个多边形具有无效的环结构，所以无效。|  
|24416|因为在曲线 {0} 开始点的边缘 {1} 是一行或具有对跖端点的退化弧不有效。|  
  
## <a name="examples"></a>示例  
 无效的空间对象的下面的示例演示如何**IsValidDetailed()**方法的行为。  
  
```sql  
DECLARE @p GEOGRAPHY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24409: Not valid because some portion of polygon ring (1) lies in the interior of a polygon.  
```  
  
## <a name="see-also"></a>另请参阅  
 [地理实例上的扩展方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
