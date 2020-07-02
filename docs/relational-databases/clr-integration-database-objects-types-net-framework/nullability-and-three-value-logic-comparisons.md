---
title: 为空性和三值逻辑比较 |Microsoft Docs
description: 本文介绍了 SQL Server 数据类型与 .NET Framework 中的类型（具有类似的语义和精度）的不同之处。
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
ms.openlocfilehash: 2c81ba685de223f213da150da0edb930385b84d5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719930"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>为 Null 性和三值逻辑比较
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  如果你熟悉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型，将会在中的**SqlTypes**命名空间中找到类似的语义和精度 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。 但是，这些数据类型之间存在一些不同之处，本主题介绍了这些不同之处中最重要的内容。  
  
## <a name="null-values"></a>NULL 值  
 本机公共语言运行时 (CLR) 数据类型和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型之间的一个主要不同就是前者不允许 NULL 值，而后者提供了完整 NULL 语义。  
  
 NULL 值对比较会产生影响。 当对 x 和 y 两个值进行比较时，如果 x 或 y 其中一个为 NULL，则某些逻辑比较将为 UNKNOWN 值而不是 True 或 False。  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 数据类型  
 **SqlTypes**命名空间引入了**SqlBoolean**类型来表示此三值逻辑。 任何**SqlTypes**之间的比较将返回**SqlBoolean**值类型。 未知值由**SqlBoolean**类型的 null 值表示。 提供了**IsTrue**、 **IsFalse**和**IsNull**属性来检查**SqlBoolean**类型的值。  
  
## <a name="operations-functions-and-null-values"></a>操作、函数和 NULL 值  
 如果 SqlTypes 的任何操作数或参数为 NULL，则所有算术运算符（+、-、 \* 、/、%）、位运算符（~、& 和 |）和大多数函数**SqlTypes**都返回 null。 **IsNull**属性始终返回 true 或 false 值。  
  
## <a name="precision"></a>精度  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中的 decimal 数据类型较 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 numeric 和 decimal 数据类型具有不同的最大值。 另外，在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，decimal 数据类型假设具有最大精度。 但在 CLR 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ， **SqlDecimal**提供的最大精度和小数位数以及与中的 decimal 数据类型相同的语义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="overflow-detection"></a>溢出检测  
 在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，两个很大的数字相加可能不会引发异常。 相反，如果未使用检查运算符，则返回的值可能作为负整数“环绕”。 在**SqlTypes**中，将针对所有溢出和下溢错误和被零除错误引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
