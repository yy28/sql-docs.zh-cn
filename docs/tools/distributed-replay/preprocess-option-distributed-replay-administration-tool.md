---
title: "Preprocess 选项 （分布式的重播管理工具） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: distributed-replay
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9b5012fd-233e-4a25-a2e1-585c63b70502
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b905204c96da26d14b31d3c62e199b3f5754720
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="preprocess-option-distributed-replay-administration-tool"></a>preprocess 选项（分布式重播管理工具）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具， **DReplay.exe**，是一个命令行工具，可用来与分布式的重播控制器进行通信。 本主题介绍 **preprocess** 命令行选项和相应的语法。  
  
 **preprocess** 选项用于启动预处理阶段。 在此阶段，控制器会准备对针对目标服务器进行重播的输入跟踪数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标")与管理工具语法结合使用的语法约定的详细信息，请参阅[TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>语法  
  
```  
  
dreplay preprocess [-m controller] -i input_trace_file  
    -d controller_working_dir [-c config_file] [-f status_interval]  
```  
  
#### <a name="parameters"></a>Parameters  
 **-m** *控制器*  
 指定控制器的计算机名称。 可以用“`localhost`”或“`.`”指代本地计算机。  
  
 如果未指定 **-m** 参数，则使用本地计算机。  
  
 **-i** *input_trace_file*  
 指定控制器上输入跟踪文件的完整路径，例如 `D:\Mytrace.trc`。 **-i** 参数是必需的。  
  
 如果同一目录中存在滚动更新文件，则会自动加载并使用这些文件。 文件必须遵循文件滚动更新命名约定，例如： `Mytrace.trc`、 `Mytrace_1.trc`、 `Mytrace_2.trc`、 `Mytrace_3.trc`、… `Mytrace_n.trc`。  
  
> [!NOTE]  
>  如果要在控制器以外的其他计算机上使用管理工具，则需要将输入跟踪文件复制到控制器上，以便可以对此参数使用本地路径。  
  
 **-d** *controller_working_dir*  
 指定控制器上用于存储中间文件的目录。 **-d** 参数是必需的。  
  
 需要满足以下要求：  
  
-   目录必须位于控制器上。  
  
-   必须指定以驱动器号开头（例如 `c:\WorkingDir`）的完整路径。  
  
-   路径不能以反斜杠“`\`”结尾。  
  
-   不支持 UNC 路径。  
  
 **-c** *config_file*  
 预处理配置文件的完整路径；当预处理配置文件存储在其他位置时，用于指定该配置文件的位置。 此参数可以是 UNC 路径，也可以是您运行管理工具的计算机上的本地路径。  
  
 如果不需要筛选，或者不想修改最大空闲时间，则 **-c** 参数不是必需的。  
  
 如果不使用 **-c** 参数，将使用默认预处理配置文件 `DReplay.exe.preprocess.config`。  
  
 **-f** *status_interval*  
 指定显示状态消息的频率（以秒为单位）。  
  
 如果未指定 **-f** ，则默认间隔为 30 秒。  
  
## <a name="examples"></a>示例  
 在本示例中，预处理阶段采用所有默认设置启动。 值 `localhost` 表示控制器服务与管理工具在同一计算机上运行。 *Input_trace_file* 参数指定输入跟踪数据的位置 `c:\mytrace.trc`。 由于不涉及跟踪文件筛选，因此必须指定 **-c** 参数。  
  
```  
dreplay preprocess –m localhost -i c:\mytrace.trc -d c:\WorkingDir  
```  
  
 在本示例中，启动了预处理阶段并指定了修改过的预处理配置文件。 与前面的示例不同， **-c** 参数用于指向修改过的配置文件（如果你将该文件存储在其他位置）。 例如：  
  
```  
dreplay preprocess –m localhost -i c:\mytrace.trc -d c:\WorkingDir -c c:\DReplay.exe.preprocess.config  
```  
  
 在修改过的预处理配置文件中，添加了筛选条件以在分布式重播期间筛选掉系统会话。 可通过修改预处理配置文件 `<PreprocessModifiers>` 中的 `DReplay.exe.preprocess.config`元素来添加筛选器。  
  
 下面是修改过的配置文件的示例：  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
## <a name="permissions"></a>权限  
 您必须作为交互用户、本地用户或域用户帐户运行管理工具。 若要使用本地用户帐户，管理工具和控制器必须在同一台计算机上运行。  
  
 有关详细信息，请参阅 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)。  
  
## <a name="see-also"></a>另请参阅  
 [准备输入跟踪数据](../../tools/distributed-replay/prepare-the-input-trace-data.md)   
 [SQL Server 分布式重播](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [配置 Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
