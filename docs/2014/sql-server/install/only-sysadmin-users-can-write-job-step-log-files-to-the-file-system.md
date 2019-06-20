---
title: 只有 sysadmin 用户可以将作业步骤日志文件写入文件系统 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84d04729e2f4c00c5d127a706727567c44855cd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093682"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>只有 sysadmin 用户才能将作业步骤日志文件写入文件系统
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 可以为每个作业步骤写入一个日志。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="description"></a>Description  
 在中[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可以将日志写入到文件系统中的成员拥有的作业**sysadmin**固定的服务器角色。 如果作业所有者不属于**sysadmin**角色并且已启用代理帐户，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可以通过使用代理帐户的凭据向文件系统写入日志。  
  
 升级不是成员的用户拥有的作业后的**sysadmin**固定的服务器角色不再可以向文件系统写入日志。 相反，这些用户可以选择将其日志写入表中的选项**msdb**数据库。 成员**sysadmin**角色仍可以对文件系统写入日志文件。  
  
## <a name="corrective-action"></a>纠正措施  
 升级不是成员的用户拥有的作业后的**sysadmin**角色将继续运行，但将不会创建日志。 若要记录到一个表，不是成员的用户的作业步骤的**sysadmin**角色必须手动更新作业。  
  
 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“创建作业”、“创建作业步骤”和“处理多个作业步骤”主题。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
