---
title: 排序规则和 CLR 集成数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 51345c498277cc7013bbc05784022f65d77aef65
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081337"
---
# <a name="collation-and-clr-integration-data-types"></a>排序规则和 CLR 集成数据类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在中[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]， **CompareInfo**对象处理排序规则。 字符串应用程序编程接口（Api）使用与当前线程的**CultureInfo**对象关联的 CompareInfo 属性来执行字符串比较。 **** [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **CultureInfo**对象的默认设置基于运行的计算机[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 Windows 区域设置。 这会确定默认的比较语义（如果没有指定显式**CultureInfo** ）来比较**system.string**值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会将**CompareInfo**属性显式更改为数据库或服务器排序规则。 如果需要，用户必须在其例程中设置相应的**CompareInfo**属性。  
  
## <a name="parameter-collation"></a>参数排序规则  
 当你创建公共语言运行时（CLR）例程，并且绑定到例程的 CLR 方法的参数为**SQLString**类型时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将使用包含调用例程的数据库的默认排序规则创建参数的实例。 如果参数不是**SqlType** （例如， **String**而不是**SQLString**），则数据库中的排序规则信息不与参数相关联。  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
