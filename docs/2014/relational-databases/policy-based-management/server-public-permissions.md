---
title: 服务器 public 权限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a0b125841e2d3c9f03b7ba46519f80af9293a1cd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026754"
---
# <a name="server-public-permissions"></a>服务器 public 权限
  此规则确定 public 服务器角色是否具有服务器权限。 在服务器上创建的每个登录名都是 public 服务器角色的成员。 如果满足此条件，则服务器上的每个登录名都将具有服务器权限。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 请勿为服务器 public 角色授予服务器权限。  
  
> [!IMPORTANT]  
>  安装程序完成后**公共**角色具有`CONNECT`之外的所有端点上的权限**专用管理员连接**。 这很正常，通常不应更改。 (访问控制通过使用`CONNECT SQL`它创建新的登录名时被自动授予的权限。)  
  
### <a name="for-more-information"></a>有关详细信息，请参阅：  
 [保护 SQL Server](../security/securing-sql-server.md)  
  
  