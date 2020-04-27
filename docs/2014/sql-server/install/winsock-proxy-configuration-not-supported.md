---
title: 不支持 Winsock 代理配置 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Winsock proxy configuration [SQL Server]
ms.assetid: abf71f7b-8bd7-49d2-92f7-9ddf72924d8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7d5daa8042e53b9bf26ad507c4be1f361821909
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66090979"
---
# <a name="winsock-proxy-configuration-not-supported"></a>不支持 Winsock 代理配置
  不能使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]工具配置 Winsock 代理。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具不能配置 Windows 组件。  
  
## <a name="corrective-action"></a>纠正措施  
 请使用 Microsoft Internet Security and Acceleration (ISA) Server 发布计算机。 有关如何配置 Winsock 代理的信息，请参阅代理服务器文档。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
