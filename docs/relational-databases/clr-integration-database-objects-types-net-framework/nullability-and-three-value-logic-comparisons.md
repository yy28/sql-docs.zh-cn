---
title: 空和三值逻辑比较 |微软文档
description: 本文介绍了 SQL Server 数据类型与 System.Data.SqlTypes 中的类型有何不同，这些类型具有相似的语义和精度。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f016abf2113afef3e02f01fd9842b91b742d50a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488434"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>为 Null 性和三值逻辑比较
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果您熟悉数据类型，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您将在**System.Data.SqlType**命名空间中找到类似的语义和精度。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 但是，这些数据类型之间存在一些不同之处，本主题介绍了这些不同之处中最重要的内容。  
  
## <a name="null-values"></a>NULL 值  
 本机公共语言运行时 (CLR) 数据类型和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型之间的一个主要不同就是前者不允许 NULL 值，而后者提供了完整 NULL 语义。  
  
 NULL 值对比较会产生影响。 当对 x 和 y 两个值进行比较时，如果 x 或 y 其中一个为 NULL，则某些逻辑比较将为 UNKNOWN 值而不是 True 或 False。  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 数据类型  
 **系统.Data.SqlType**命名空间引入了**SqlBoolean**类型来表示此 3 值逻辑。 任何**SqlType**之间的比较都返回**SqlBoolean**值类型。 未知值由**SqlBoolean**类型的空值表示。 提供属性**IsTrue** **、IsFalse**和**IsNull**用于检查**SqlBoolean**类型的值。  
  
## <a name="operations-functions-and-null-values"></a>操作、函数和 NULL 值  
 所有算术运算符（+、-、/、%）\*位运算符（*、& 和 *），如果**SqlTypes**的任何操作数或参数为 NULL，则大多数函数将返回 NULL。 **IsNull**属性始终返回真值或假值。  
  
## <a name="precision"></a>Precision  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中的 decimal 数据类型较 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 numeric 和 decimal 数据类型具有不同的最大值。 另外，在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，decimal 数据类型假设具有最大精度。 但是，在 的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR 中 **，SqlDecimal**提供了与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的十进制数据类型相同的最大精度和比例，以及相同的语义。  
  
## <a name="overflow-detection"></a>溢出检测  
 在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，两个很大的数字相加可能不会引发异常。 相反，如果未使用检查运算符，则返回的值可能作为负整数“环绕”。 在**System.Data.SqlTypes 中**，对所有溢出和下溢错误以及除以零的错误都引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
