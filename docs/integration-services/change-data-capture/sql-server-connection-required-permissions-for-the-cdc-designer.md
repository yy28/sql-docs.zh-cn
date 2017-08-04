---
title: "针对 CDC 设计器 SQL Server 连接所需的权限 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bdcee015ce6c936b3fc8b8653b21208bdee31074
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>针对 CDC 设计器的 SQL Server 连接所需权限
  CDC 设计器控制台需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接信息以便执行其任务。 本主题介绍可在 **“连接到 SQL Server”** 对话框中为设置与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的连接而提供的信息。  
  
 **“连接到 SQL Server”** 对话框将在需要时打开，例如在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接信息不可用时或者在该信息存在但连接没有所需权限时。  
  
 下表介绍需要连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的不同任务以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名/用户的所需权限。  
  
|任务|最低权限|  
|----------|-------------------------|  
|查看使用关联的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 CDC 服务和实例的列表。|`db_datareader` 角色|  
|启动/停止 CDC 实例|`db_datareader` 和 `db_datawriter` 角色|  
|查看 CDC 实例状态。|`db_owner` 角色|  
|创建新的 Oracle CDC 实例数据库。|`dbcreator` 固定服务器角色|  
|创建新的 Oracle CDC 实例。|`db_datareader` 角色<br /><br /> `db_owner` 角色。|  
|获取部署脚本。|`db_datareader` 和 `db_datawriter` 角色<br /><br /> `db_owner` 角色|  
|更改配置和添加/删除捕获实例。|`db_datareader` 和 `db_datawriter` 角色<br /><br /> `db_owner` 角色|  
  
## <a name="see-also"></a>另请参阅  
 [访问 CDC 设计器控制台](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [SQL Server Connection for Instance Creation](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
