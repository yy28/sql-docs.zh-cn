---
title: 对用户数据库的 Guest 权限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 325242c6660aa49c9358399b38c92d72e21aaf46
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705122"
---
# <a name="guest-permissions-on-user-databases"></a>对用户数据库的 Guest 权限
  此规则确定 guest 用户是否有权访问数据库。 此规则仅适用于用户数据库。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 如果 guest 用户不需要访问数据库，请撤消其访问数据库的权限。  
  
 不能删除 guest 用户，但可在除 master、tempdb 或 msdb 之外的任何数据库中执行 REVOKE CONNECT FROM GUEST 来撤消它的 CONNECT 权限，从而禁用 guest 用户。  
  
## <a name="for-more-information"></a>有关详细信息  
 [保护 SQL Server](../security/securing-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
