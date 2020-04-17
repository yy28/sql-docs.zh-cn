---
title: 排序和 CLR 集成数据类型 |微软文档
description: 在 SQL Server CLR 集成中，.NET 框架字符串 API 使用当前线程的"文化信息"的 CompareInfo 属性执行字符串比较。
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
ms.openlocfilehash: 46e4d450db90e4bfc93187a48ca8adae472036c6
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488474"
---
# <a name="collation-and-clr-integration-data-types"></a>排序规则和 CLR 集成数据类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]中，**比较信息**对象处理排序规则。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]字符串应用程序编程接口 （API） 使用与当前线程的**区域性信息**对象关联的**CompareInfo**属性执行字符串比较。 **区域性信息**对象的默认设置基于正在运行的计算机[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 Windows 区域设置。 这将确定默认比较语义（如果未指定显式**区域性信息**）用于**比较 System.String**值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会显式将**CompareInfo**属性更改为数据库或服务器排序规则。 如果需要，用户必须在其例程中设置相应的**比较信息**属性。  
  
## <a name="parameter-collation"></a>参数排序规则  
 当您创建通用语言运行时 （CLR） 例程时，绑定到例程的 CLR 方法的参数是**SQLString**类型，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建参数的实例，其中包含调用例程的数据库的默认排序。 如果参数不是**SqlType（** 例如，**字符串**而不是**SQLString），** 则数据库中的排序规则信息不与参数相关联。  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
