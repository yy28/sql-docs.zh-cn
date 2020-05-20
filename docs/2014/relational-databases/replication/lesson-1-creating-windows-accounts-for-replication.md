---
title: 第 1 课：为复制创建 Windows 帐户 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
- replication [SQL Server], administering
ms.assetid: 65c3816b-47f0-448c-a4a4-ebd3e2a58820
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f11321b20c4238fdf9b3376d79edcb12c0e9204b
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000465"
---
# <a name="lesson-1-creating-windows-accounts-for-replication"></a>第 1 课：为复制创建 Windows 帐户
  在本课中，将创建 Windows 帐户以运行复制代理。 您将在本地服务器上为以下代理创建一个单独的 Windows 帐户：  
  
|Agent|位置|帐户名|  
|-----------|--------------|------------------|  
|快照代理|Publisher|\<*machine_name*>\repl_snapshot|  
|日志读取器代理|Publisher|\<*machine_name*>\repl_logreader|  
|分发代理|发布服务器和订阅服务器|\<*machine_name*>\repl_distribution|  
|合并代理|发布服务器和订阅服务器|\<*machine_name*>\repl_merge|  
  
> [!NOTE]  
>  在复制教程中，发布服务器和分发服务器共享同一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 发布服务器和订阅服务器可以共享同一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，但这不是必须的。 如果发布服务器和订阅服务器共享同一实例，则在订阅服务器上用于创建帐户的步骤不是必须的。  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>在发布服务器上为复制代理创建本地 Windows 帐户  
  
1.  在发布服务器上，从 "控制面板" 的 "**管理工具**" 中打开 "**计算机管理**"。  
  
2.  在“系统工具”**** 中，展开“本地用户和组”****。  
  
3.  右键单击 "**用户**"，然后单击 "**新建用户**"。  
  
4.  `repl_snapshot`在 "**用户名**" 框中输入，提供密码和其他相关信息，然后单击 "**创建**" 创建 repl_snapshot 帐户。  
  
5.  重复上述步骤创建 repl_logreader、repl_distribution 和 repl_merge 帐户。  
  
6.  单击 **“关闭”** 。  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>在订阅服务器上为复制代理创建本地 Windows 帐户  
  
1.  在订阅服务器上，从 "控制面板" 的 "**管理工具**" 中打开 "**计算机管理**"。  
  
2.  在“系统工具”**** 中，展开“本地用户和组”****。  
  
3.  右键单击 "**用户**"，然后单击 "**新建用户**"。  
  
4.  `repl_distribution`在 "**用户名**" 框中输入，提供密码和其他相关信息，然后单击 "**创建**" 创建 repl_distribution 帐户。  
  
5.  重复上述步骤创建 repl_merge 帐户。  
  
6.  单击 **“关闭”** 。  
  
## <a name="next-steps"></a>后续步骤  
 您已经成功地为复制代理创建了 Windows 帐户。 接下来，您将配置快照文件夹。 请参阅 [第 2 课：准备快照文件夹](lesson-2-preparing-the-snapshot-folder.md)。  
  
## <a name="see-also"></a>另请参阅  
 [复制代理概述](agents/replication-agents-overview.md)  
  
  
