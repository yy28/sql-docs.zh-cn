---
title: "排序规则和 CLR 集成数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 19ce71cdffe3272a791cf7f9961a4d7757c913ff
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="collation-and-clr-integration-data-types"></a>排序规则和 CLR 集成数据类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]、 **compareinfo 一起**对象处理通过排序规则。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]字符串编程接口 (Api) 使用的应用程序**compareinfo 一起**与关联属性**CultureInfo**当前线程来执行字符串比较的对象。 默认设置**CultureInfo**对象基于[!INCLUDE[msCoName](../../includes/msconame-md.md)]的计算机上的 Windows 区域设置[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 这将确定默认的比较语义，如果不显式**CultureInfo** ，为指定的比较**System.String**值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会显式更改**compareinfo 一起**到数据库或服务器排序规则的属性。 如果需要，用户必须设置相应**compareinfo 一起**其例程中的属性。  
  
## <a name="parameter-collation"></a>参数排序规则  
 当你创建的公共语言运行时 (CLR) 例程，并将 CLR 方法的参数绑定到的类型是例程**SQLString**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建具有数据库的默认排序规则的参数实例包含调用的例程。 如果参数不是**SqlType** (例如，**字符串**而非**SQLString**)，从数据库的排序规则信息不与参数相关联。  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
