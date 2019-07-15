---
title: 取消选项（Distributed Replay 管理工具）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: fea376de-307a-4b45-b7e2-37df88f3681a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a03a7cc6182d2196195b73a3a8010cbbcda60920
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732179"
---
# <a name="cancel-option-distributed-replay-administration-tool"></a>Cancel 选项（分布式重播管理工具）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具 **DReplay.exe** 是一个命令行工具，可与分布式重播控制器一起用来进行通信。 本主题介绍 **cancel** 命令行选项和相应的语法。  
  
 **cancel** 选项取消控制器上运行的当前操作。  
  
 ![主题连接图标](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") 有关与此管理工具语法结合使用的语法约定的详细信息，请参阅 [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
dreplay cancel [-m controller] [-q]   
```  
  
#### <a name="parameters"></a>Parameters  
 **-m** *控制器*  
 控制器的计算机名称。 可以用“`localhost`”或“`.`”指代本地计算机。  
  
 如果未指定 **-m** 参数，则使用本地计算机。  
  
 **-q**  
 静默模式。 不提示进行确认。  
  
 **-q** 参数是可选的。  
  
## <a name="examples"></a>示例  
 在下面的示例中，在静默模式下提交一个取消请求。 值 `localhost` 表示控制器服务与管理工具在同一计算机上运行。  
  
```  
dreplay cancel -m localhost -q  
```  
  
## <a name="permissions"></a>权限  
 您必须作为交互用户、本地用户或域用户帐户运行管理工具。 若要使用本地用户帐户，管理工具和控制器必须在同一台计算机上运行。  
  
 有关详细信息，请参阅 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 分布式重播](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
