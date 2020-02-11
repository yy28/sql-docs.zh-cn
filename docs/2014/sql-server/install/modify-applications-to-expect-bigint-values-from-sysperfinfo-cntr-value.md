---
title: 修改应用程序，使其 sysperfinfo 中出现 bigint 值。 cntr_value |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sysperfinfo
- bigint values [SQL Server]
ms.assetid: b0345303-6e9a-4078-8148-6e1bce207b8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ced1e07b5423dcdc7c13d24e8528a2b6ac240aaa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093961"
---
# <a name="modify-applications-to-expect-bigint-values-from-sysperfinfocntr_value"></a>修改应用程序以期望从 sysperfinfo.cntr_value 获取 bigint 值
  sysperfinfo 为 cntr_value `bigint`列返回值。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 请修改使用 sysperfinfo 的应用程序，确保它们可以处理 cntr_value 列的 `bigint` 值。  
  
> [!NOTE]  
>  sysperfinfo 是一个兼容性视图。 应改用 sys.dm_os_performance_counter 动态管理视图。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
