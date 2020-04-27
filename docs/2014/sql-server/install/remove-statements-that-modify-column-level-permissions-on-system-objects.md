---
title: 删除对系统对象的列级权限进行修改的语句 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- column-level permissions [SQL Server]
- removed statement permissions [SQL Server]
ms.assetid: 7f4fbbef-2696-4911-903b-63f6d9e4484a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b377ac0b9baacdab6461a0e62174538902939bd8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093033"
---
# <a name="remove-statements-that-modify-column-level-permissions-on-system-objects"></a>删除用来修改系统对象的列级权限的语句
  升级顾问检测到对系统对象的非标准列级权限。 升级时将不保留这些权限更改。 此外，不再支持对系统对象的列级权限。 请从您的应用程序中删除对系统对象设置列级权限的语句。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 从应用程序中删除授予、拒绝或撤消对系统对象的列级权限的语句。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
