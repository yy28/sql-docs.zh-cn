---
title: 修改应用程序以期望从 sysperfinfo.cntr_value 获取 bigint 值 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- sysperfinfo
- bigint values [SQL Server]
ms.assetid: b0345303-6e9a-4078-8148-6e1bce207b8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4f7945a5657cefb43af402523a6aee3e12eb63a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137527"
---
# <a name="modify-applications-to-expect-bigint-values-from-sysperfinfocntrvalue"></a>修改应用程序以期望从 sysperfinfo.cntr_value 获取 bigint 值
  sysperfinfo 返回`bigint`cntr_value 列的值。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 请修改使用 sysperfinfo 的应用程序，确保它们可以处理 cntr_value 列的 `bigint` 值。  
  
> [!NOTE]  
>  sysperfinfo 是一个兼容性视图。 应改用 sys.dm_os_performance_counter 动态管理视图。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
