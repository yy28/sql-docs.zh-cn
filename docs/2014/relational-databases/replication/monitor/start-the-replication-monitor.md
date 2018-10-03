---
title: 启动复制监视器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, starting
ms.assetid: e037bd27-cc87-4ee9-9e5f-83f6d717cfa4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc5946fffd3c7417aa3afa04eeecfe01123d9fcc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48107198"
---
# <a name="start-the-replication-monitor"></a>启动复制监视器
  可以从任何 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 实例上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中启动复制监视器，也可以在命令提示符下启动复制监视器。 启动复制监视器后，将发布服务器添加至监视器。 有关详细信息，请参阅 [从复制监视器中添加和删除发布服务器](add-and-remove-publishers-from-replication-monitor.md)。  
  
### <a name="to-start-replication-monitor-from-sql-server-management-studio"></a>从 SQL Server Management Studio 启动复制监视器  
  
1.  连接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]实例，然后展开服务器节点。  
  
2.  右键单击 **“复制”** 文件夹或它的任一子文件夹，然后单击 **“启动复制监视器”**。  
  
### <a name="to-start-replication-monitor-from-the-command-prompt"></a>从命令提示符启动复制监视器  
  
1.  在命令提示符下，导航到工具安装目录。 默认路径为 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]Tools\Binn\。  
  
2.  运行 sqlmonitor.exe。  
  
## <a name="see-also"></a>请参阅  
 [监视复制](../monitoring-replication.md)  
  
  
