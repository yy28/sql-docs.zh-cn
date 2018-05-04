---
title: 为 null 性和三值逻辑比较 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cf4eb07bb901fa9657f5533847b5a07334526bc2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="nullability-and-three-value-logic-comparisons"></a>为 Null 性和三值逻辑比较
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果你熟悉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型，你将找到相似的语义和精度**System.Data.SqlTypes**中的命名空间[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。 但是，这些数据类型之间存在一些不同之处，本主题介绍了这些不同之处中最重要的内容。  
  
## <a name="null-values"></a>NULL 值  
 本机公共语言运行时 (CLR) 数据类型和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型之间的一个主要不同就是前者不允许 NULL 值，而后者提供了完整 NULL 语义。  
  
 NULL 值对比较会产生影响。 当对 x 和 y 两个值进行比较时，如果 x 或 y 其中一个为 NULL，则某些逻辑比较将为 UNKNOWN 值而不是 True 或 False。  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 数据类型  
 **System.Data.SqlTypes**命名空间引入了**SqlBoolean**类型来表示此 3 值逻辑。 任何之间的比较**SqlTypes**返回**SqlBoolean**值类型。 未知的值由的 null 值表示**SqlBoolean**类型。 属性**IsTrue**， **IsFalse**，和**IsNull**提供要检查的值**SqlBoolean**类型。  
  
## <a name="operations-functions-and-null-values"></a>操作、函数和 NULL 值  
 所有算术运算符 (+、-， \*，/、 %)，按位运算符 (~、 &、 和 |)，和大多数函数都返回 NULL 如果任何操作数或自变量**SqlTypes**均为 NULL。 **IsNull**属性始终返回 true 或 false 值。  
  
## <a name="precision"></a>精度  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中的 decimal 数据类型较 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 numeric 和 decimal 数据类型具有不同的最大值。 另外，在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，decimal 数据类型假设具有最大精度。 中的 CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但**SqlDecimal**提供相同的最大精度和小数位数，以及与中的十进制数据类型相同的语义[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="overflow-detection"></a>溢出检测  
 在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，两个很大的数字相加可能不会引发异常。 相反，如果未使用检查运算符，则返回的值可能作为负整数“环绕”。 在**System.Data.SqlTypes**，所有溢出和下溢错误和被零除错误都引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
