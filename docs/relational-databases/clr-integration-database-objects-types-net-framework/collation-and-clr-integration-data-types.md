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
manager: craigg
ms.openlocfilehash: f99bb2f8aac2278fd25713ce43e23e1a5f1d14a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678305"
---
# <a name="collation-and-clr-integration-data-types"></a>排序规则和 CLR 集成数据类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在中[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，则**CompareInfo**对象处理排序规则。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]字符串的应用程序编程接口 (Api) 使用**CompareInfo**与关联的属性**CultureInfo**当前线程来执行字符串比较的对象。 默认设置**CultureInfo**对象所基于[!INCLUDE[msCoName](../../includes/msconame-md.md)]的计算机上的 Windows 区域设置[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 这可在未显式确定默认比较语义**CultureInfo** ，为指定的比较**System.String**值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会显式更改**CompareInfo**数据库或服务器排序规则的属性。 如果需要，用户必须设置适当**CompareInfo**其例程中的属性。  
  
## <a name="parameter-collation"></a>参数排序规则  
 当你创建公共语言运行时 (CLR) 例程，并且 CLR 方法的参数绑定到的类型是例程**SQLString**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]参数的实例创建数据库的默认排序规则包含调用例程。 如果参数不是**SqlType** (例如，**字符串**而非**SQLString**)，从数据库的排序规则信息不是与参数相关联。  
  
## <a name="see-also"></a>请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
