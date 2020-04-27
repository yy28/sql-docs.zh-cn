---
title: 只有 sysadmin 用户才能将作业步骤日志文件写入文件系统 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093682"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>只有 sysadmin 用户才能将作业步骤日志文件写入文件系统
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 可以为每个作业步骤写入一个日志。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
## <a name="description"></a>说明  
 在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，对于由**sysadmin**固定服务器角色的成员所拥有的作业，代理可以将日志写入文件系统。 如果作业所有者不是**sysadmin**角色的成员，并且如果启用了代理帐户， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]则代理可以使用代理帐户的凭据将日志写入文件系统。  
  
 升级后，不属于**sysadmin**固定服务器角色成员的用户所拥有的作业将无法再将日志写入文件系统。 相反，这些用户可以选择将其日志写入**msdb**数据库中的表的选项。 **Sysadmin**角色的成员仍可以将日志文件写入文件系统。  
  
## <a name="corrective-action"></a>纠正措施  
 升级后，不属于**sysadmin**角色成员的用户所拥有的作业将继续运行，但不会创建日志。 若要将作业步骤记录到表中，不是**sysadmin**角色成员的用户必须手动更新其作业。  
  
 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“创建作业”、“创建作业步骤”和“处理多个作业步骤”主题。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 代理升级问题](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
