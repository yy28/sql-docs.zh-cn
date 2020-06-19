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
ms.openlocfilehash: 359399852224923d0512372d13058535fdca3c7c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065056"
---
# <a name="winsock-proxy-configuration-not-supported"></a>不支持 Winsock 代理配置
  不能使用工具配置 Winsock 代理 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具不能配置 Windows 组件。  
  
## <a name="corrective-action"></a>纠正措施  
 请使用 Microsoft Internet Security and Acceleration (ISA) Server 发布计算机。 有关如何配置 Winsock 代理的信息，请参阅代理服务器文档。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
