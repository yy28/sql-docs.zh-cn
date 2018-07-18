---
title: 排序规则和 CLR 集成数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 56206f6273b413a66a72b2a2c72ed3593b2f9a66
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37354679"
---
# <a name="collation-and-clr-integration-data-types"></a>排序规则和 CLR 集成数据类型
  在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中，`CompareInfo` 对象处理排序规则。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 字符串应用程序编程接口 (API) 使用与当前线程的 `CompareInfo` 对象关联的 `CultureInfo` 属性来执行字符串比较。 默认设置`CultureInfo`对象所基于[!INCLUDE[msCoName](../../includes/msconame-md.md)]的计算机上的 Windows 区域设置[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 该设置在未显式指定 `CultureInfo` 的情况下确定比较 `System.String` 值的默认比较语义。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会显式更改数据库或服务器排序规则的 `CompareInfo` 属性 用户必须根据需要在其例程中设置相应的 `CompareInfo` 属性。  
  
## <a name="parameter-collation"></a>参数排序规则  
 当创建公共语言运行时 (CLR) 例程时，如果绑定到该例程的 CLR 方法的参数类型为 `SQLString`，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 则创建一个参数实例，该实例采用包含调用例程的数据库的默认排序规则。 如果参数不是 `SqlType`（例如，该类型为 `String` 而不是 `SQLString`），数据库的排序规则信息则不与该参数关联。  
  
## <a name="see-also"></a>请参阅  
 [.NET Framework 中的 SQL Server 数据类型](sql-server-data-types-in-the-net-framework.md)  
  
  
