---
title: 状态选项（Distributed Replay 管理工具）| Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09e8ad6b60dfc9afbb3fbed7ef450dc4fb1cc28a
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589201"
---
# <a name="status-option-distributed-replay-administration-tool"></a>Status 选项（分布式重播管理工具）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具 **DReplay.exe** 是一个命令行工具，可与分布式重播控制器一起用来进行通信。 本主题介绍 **status** 命令行选项和相应的语法。  
  
 **status** 选项查询该控制器并显示当前状态。  
  
 ![主题连接图标](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") 有关与此管理工具语法结合使用的语法约定的详细信息，请参阅 [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### <a name="parameters"></a>Parameters  
 **-m** _控制器_  
 指定控制器的计算机名称。 可以用“`localhost`”或“`.`”指代本地计算机。  
  
 如果未指定 **-m** 参数，则使用本地计算机。  
  
 **-f** _status_interval_  
 指定显示状态的频率（以秒为单位）。  
  
 如果未指定 **-f** 参数，则默认间隔为 30 秒。  
  
## <a name="examples"></a>示例  
 在下面的示例中，每 60 秒显示一次当前状态。 值 `localhost` 表示控制器服务与管理工具在同一计算机上运行。  
  
```  
dreplay status -m localhost -f 60  
```  
  
## <a name="permissions"></a>Permissions  
 您必须作为交互用户、本地用户或域用户帐户运行管理工具。 若要使用本地用户帐户，管理工具和控制器必须在同一台计算机上运行。  
  
 有关详细信息，请参阅 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 分布式重播](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Transact-SQL 调试器](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
