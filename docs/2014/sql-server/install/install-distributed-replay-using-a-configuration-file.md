---
title: 使用配置文件安装 Distributed 的 Replay |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3259232c-6963-4c9c-9d10-ae42aa262eef
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9db8127a9a43478d891d5955190bd594fb6647b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094576"
---
# <a name="install-distributed-replay-using-a-configuration-file"></a>使用配置文件安装 Distributed Replay
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序提供基于用户输入和系统默认值生成配置文件的功能。 如果您指定要安装管理工具，则可以使用配置文件来部署三个 Distributed Replay 组件（管理工具、Distributed Replay 控制器和 Distributed Replay 客户端）。 它支持安装、修复和卸载 Distributed Replay 组件。  
  
 安装程序仅支持通过命令行使用配置文件。 下面列出了在使用配置文件时参数的处理顺序：  
  
-   配置文件覆盖包中的默认值  
  
-   命令行的值覆盖配置文件中的值  
  
 有关如何使用配置文件的详细信息，请参阅[使用安装 SQL Server 2014 配置文件](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)。  
  
> [!IMPORTANT]  
>  安装 Distributed Replay 之后，您必须在控制器和客户端计算机上创建防火墙规则，并授予每台客户端计算机对目标服务器的权限。 有关详细信息，请参阅 [完成安装后步骤](../../tools/distributed-replay/complete-the-post-installation-steps.md)。  
  
### <a name="to-generate-a-configuration-file"></a>生成配置文件  
  
1.  按照安装向导的说明操作，直到出现 **“准备安装”** 页面。 配置文件的路径是在 **“准备安装”** 页的配置文件路径部分中指定的。  
  
2.  取消安装并且不要真正完成安装，以便生成 INI 文件。  
  
### <a name="to-install-distributed-replay-using-the-configuration-file"></a>使用配置文件安装 Distributed Replay  
  
-   通过命令提示符运行安装并使用 ConfigurationFile 参数提供 ConfigurationFile.ini。  
  
 **示例语法**  
  
 下面是如何在命令提示符处指定配置文件的示例：  
  
```  
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```  
  
> [!NOTE]  
>  您必须在命令行中指定这两个密码，因为您无法在配置文件中配置这些密码。  
  
  
