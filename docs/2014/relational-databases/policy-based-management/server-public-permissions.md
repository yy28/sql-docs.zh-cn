---
title: 服务器 public 权限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 11f478f9cbbdedd246b3b1468572b62b27c86e5b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207907"
---
# <a name="server-public-permissions"></a>服务器 public 权限
  此规则确定 public 服务器角色是否具有服务器权限。 在服务器上创建的每个登录名都是 public 服务器角色的成员。 如果满足此条件，则服务器上的每个登录名都将具有服务器权限。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 请勿为服务器 public 角色授予服务器权限。  
  
> [!IMPORTANT]  
>  安装程序完成后**公共**角色具有`CONNECT`之外的所有端点上的权限**专用管理员连接**。 这很正常，通常不应更改。 (通过使用控制访问`CONNECT SQL`创建新的登录名时自动授予的权限。)  
  
### <a name="for-more-information"></a>有关详细信息，请参阅：  
 [保护 SQL Server](../security/securing-sql-server.md)  
  
  
