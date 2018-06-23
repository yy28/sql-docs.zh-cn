---
title: 仅 sysadmin 用户可以将作业步骤日志文件写入到文件系统 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e0b7638bbbf33cdd820467cd21edc40a6f5c42ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028702"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>只有 sysadmin 用户才能将作业步骤日志文件写入文件系统
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 可以为每个作业步骤写入一个日志。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="description"></a>Description  
 在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可以将日志写入的文件系统的成员拥有的作业， **sysadmin**固定的服务器角色。 如果作业所有者不是成员的**sysadmin**角色并且已启用的代理帐户，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可以通过使用代理帐户的凭据向文件系统写入日志。  
  
 升级不是成员的用户所拥有的作业之后的**sysadmin**固定的服务器角色可以不再日志写入文件系统。 相反，这些用户可以选择将其日志写入表中**msdb**数据库。 成员**sysadmin**角色仍然可以将日志文件写入到文件系统。  
  
## <a name="corrective-action"></a>纠正措施  
 升级不是成员的用户所拥有的作业之后的**sysadmin**角色将继续运行，但将不会创建日志。 若要登录到一个表，而不是成员的用户的作业步骤的**sysadmin**角色必须手动更新其工作。  
  
 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“创建作业”、“创建作业步骤”和“处理多个作业步骤”主题。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  