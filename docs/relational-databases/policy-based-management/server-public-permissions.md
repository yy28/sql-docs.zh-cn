---
title: "服务器 public 权限 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d5c9c5606ffe070cd72648e256f059d6375455dd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="server-public-permissions"></a>服务器 public 权限
  此规则确定 public 服务器角色是否具有服务器权限。 在服务器上创建的每个登录名都是 public 服务器角色的成员。 如果满足此条件，则服务器上的每个登录名都将具有服务器权限。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 请勿为服务器 public 角色授予服务器权限。  
  
> [!IMPORTANT]  
>  安装完成后， **PUBLIC** 角色在“专用管理员连接”  之外的所有端点上具有 **CONNECT**权限。 这很正常，通常不应更改。 （通过使用 **CONNECT SQL** 权限来控制访问，该权限是在创建新登录名时自动授予的。）  
  
### <a name="for-more-information"></a>有关详细信息，请参阅：  
 [保护 SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
  
