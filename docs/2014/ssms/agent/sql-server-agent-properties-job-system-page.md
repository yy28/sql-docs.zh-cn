---
title: SQL Server 代理属性（“作业系统”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 56a91e0be9e85bdc3042fc5cf798c3965f6322ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129120"
---
# <a name="sql-server-agent-properties-job-system-page"></a>SQL Server 代理属性（“作业系统”页）
  使用此页可以查看和修改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务管理作业的方式。  
  
## <a name="options"></a>“常规”  
 **关闭超时间隔(秒)**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在关闭作业之前等待作业完成的秒数。 如果在指定间隔之后作业仍在运行，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将强制停止该作业。  
  
 **使用非管理员代理帐户**  
 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理设置非管理员代理帐户。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本支持多个代理，因此，仅当管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]代理版本时此选项才适用。  
  
 **用户名**  
 键入非管理员代理帐户的用户名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持多个代理，所以仅当管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]代理版本时此选项才适用。  
  
 **密码**  
 键入非管理员代理帐户的用户密码。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本支持多个代理，因此，仅当管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]代理版本时此选项才适用。  
  
 **域**  
 键入非管理性代理帐户的用户域。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持多个代理，所以仅当管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]代理版本时此选项才适用。  
  
## <a name="see-also"></a>请参阅  
 [执行作业](implement-jobs.md)  
  
  