---
title: "管理工具命令行选项 （分布式的重播实用工具） |Microsoft 文档"
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: distributed-replay
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c01b0ed3-67e4-4561-92d2-a8fbb086aca8
caps.latest.revision: "35"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac0fe5fe3686e60ef16d95899c69ecd72742e850
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="administration-tool-command-line-options-distributed-replay-utility"></a>管理工具命令行选项（分布式重播实用工具）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具， **DReplay.exe**，是命令行工具，用于与分布式的重播控制器进行通信。 可使用此管理工具在控制器上启动、监视和取消操作。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标")与管理工具语法结合使用的语法约定的详细信息，请参阅[TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>语法  
  
```  
  
dreplay {preprocess|replay|status|cancel} [options] [-?]}  
  
Usage:  
  
  dreplay preprocess [-m controller] -i input_trace_file  
    -d controller_working_dir [-c config_file] [-f status_interval]  
  
  dreplay replay [-m controller] -d controller_working_dir [-o]  
    [-s target_server] -w clients [-c config_file]  
    [-f status_interval]  
  
  dreplay status [-m controller] [-f status_interval]  
  
  dreplay cancel [-m controller] [-q]   
```  
  
## <a name="remarks"></a>注释  
 你可以使用 **DReplay.exe**发出以下命令行选项：  
  
 **preprocess**  
 启动预处理阶段。 控制器准备您从生产环境中捕获的输入跟踪数据，以便对目标服务器进行重播。  
  
 **replay**  
 启动事件重播阶段。 控制器将重播数据调度到指定客户端，启动分布式重播并同步客户端。 每个选定的客户端可以选择记录重播活动并在本地保存结果跟踪文件。  
  
 **status**  
 查询控制器并显示当前状态。  
  
 **cancel**  
 取消正在控制器上运行的当前操作。  
  
 对于包含命令参数和示例的详细语法信息，请参阅下列主题：  
  
-   [预处理选项 &#40; 分布式的重播管理工具 &#41;](../../tools/distributed-replay/preprocess-option-distributed-replay-administration-tool.md)  
  
-   [重播选项 &#40; 分布式的重播管理工具 &#41;](../../tools/distributed-replay/replay-option-distributed-replay-administration-tool.md)  
  
-   [状态选项 &#40; 分布式的重播管理工具 &#41;](../../tools/distributed-replay/status-option-distributed-replay-administration-tool.md)  
  
-   [取消选项 &#40; 分布式的重播管理工具 &#41;](../../tools/distributed-replay/cancel-option-distributed-replay-administration-tool.md)  
  
 RPC 将作为 RPC 而非语言事件进行重播。  
  
## <a name="permissions"></a>权限  
 您必须作为交互用户、本地用户或域用户帐户运行管理工具。 若要使用本地用户帐户，管理工具和控制器必须在同一台计算机上运行。  
  
 有关详细信息，请参阅 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 分布式重播](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
