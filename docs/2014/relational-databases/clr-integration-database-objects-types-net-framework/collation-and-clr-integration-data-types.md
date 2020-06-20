---
title: 排序规则和 CLR 集成数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a5b0367487aeb80355b8c5c976818e1b6c1ac04
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954837"
---
# <a name="collation-and-clr-integration-data-types"></a>排序规则和 CLR 集成数据类型
  在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中，`CompareInfo` 对象处理排序规则。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 字符串应用程序编程接口 (API) 使用与当前线程的 `CompareInfo` 对象关联的 `CultureInfo` 属性来执行字符串比较。 对象的默认设置 `CultureInfo` 基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 运行的计算机的 Windows 区域设置 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 该设置在未显式指定 `CultureInfo` 的情况下确定比较 `System.String` 值的默认比较语义。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会显式更改数据库或服务器排序规则的 `CompareInfo` 属性 用户必须根据需要在其例程中设置相应的 `CompareInfo` 属性。  
  
## <a name="parameter-collation"></a>参数排序规则  
 当创建公共语言运行时 (CLR) 例程时，如果绑定到该例程的 CLR 方法的参数类型为 `SQLString`，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 则创建一个参数实例，该实例采用包含调用例程的数据库的默认排序规则。 如果参数不是 `SqlType`（例如，该类型为 `String` 而不是 `SQLString`），数据库的排序规则信息则不与该参数关联。  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](sql-server-data-types-in-the-net-framework.md)  
  
  
