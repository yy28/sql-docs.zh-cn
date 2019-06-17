---
title: 数据库引擎配置-用户实例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- database engine configuration
- database engine configuration, user instance
ms.assetid: dfc27c1e-0fe2-4221-bed5-f52667ddd3c8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ba05d426f9515793ad3a924e375ff9a6ab9f940f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095882"
---
# <a name="database-engine-configuration---user-instance"></a>数据库引擎配置 - 用户实例
  使用 **“用户实例”** 页可以为不具有管理员权限的用户生成单独的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并可以将用户添加到管理员角色中。  
  
## <a name="option"></a>Option  
 启用用户实例  
 默认值为“启用”。 若要禁用用户实例的功能，请清除此复选框。  
  
 用户实例也称为子实例或客户端实例，是由父实例（作为服务运行的主实例，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ）代表用户生成的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]实例。 用户实例作为用户进程在该用户的安全上下文中运行。 用户实例独立于父实例和该计算机上运行的任何其他用户实例。 用户实例功能也称为“作为正常用户运行”(RANU)。  
  
> [!NOTE]  
>  在安装过程中设置为 **sysadmin** 固定服务器角色的成员的登录名都设置为模板数据库中的管理员。 除非被删除，否则它们是用户实例的 **sysadmin** 固定服务器角色的成员。  
  
 将用户添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员角色中  
 默认情况下不启用此选项。 若要将当前安装用户添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员角色中，请选中此复选框。  
  
 作为 BUILTIN\Administrators 成员的 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 用户在连接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 时，不会自动添加到 sysadmin 固定服务器角色中。 只有已显式添加到服务器级管理员角色中的 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 用户才能管理 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 Built-In\Users 组的任一成员都可连接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 实例，但他们仅拥有执行数据库任务的有限权限。 因此，对于从先前 Windows 版本中的 BUILTIN\Administrators 和 Built-In\Users 继承 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 特权的用户，必须在运行于 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 上的 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]实例中为其显式授予管理特权。  
  
 若要在此安装程序完成后对用户角色进行任何更改，请使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 外围应用配置器工具 (SQLSAC.exe)。 若要更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员角色中的用户列表，请单击 **“添加新管理员”** 链接。  
  
 确保“要设置的用户”  字段中列出了应更新其权限的用户的 DomainName\UserName。 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] “可用权限” **窗格的** 实例列表中选择要更新的角色，然后单击向右箭头。 若要将用户添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的所有可用实例的所有可用角色中，请单击向右双箭头。  
  
 若要在完成选择后实现这些更改， [!INCLUDE[clickOK](../../includes/clickok-md.md)]。 若要在不进行更改的情况下结束使用此工具，请单击 **“取消”** 。  
  
  
