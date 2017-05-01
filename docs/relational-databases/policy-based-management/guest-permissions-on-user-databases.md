---
title: "对用户数据库的 Guest 权限 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8ff6a7d05a37ed4c0c22c3533df1aa040a116c32
ms.lasthandoff: 04/11/2017

---
# <a name="guest-permissions-on-user-databases"></a>对用户数据库的 Guest 权限
  此规则确定 guest 用户是否有权访问数据库。 此规则仅适用于用户数据库。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 如果 guest 用户不需要访问数据库，请撤消其访问数据库的权限。  
  
 不能删除 guest 用户，但可在除 master、tempdb 或 msdb 之外的任何数据库中执行 REVOKE CONNECT FROM GUEST 来撤消它的 CONNECT 权限，从而禁用 guest 用户。  
  
## <a name="for-more-information"></a>有关详细信息  
 [保护 SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
