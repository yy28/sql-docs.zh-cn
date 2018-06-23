---
title: 准备输入的跟踪数据 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c14fd3d2-5770-47c2-a851-cc13ddbc9bf5
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 30b9108a8586e56f7a96695be513e6e33fe39c85
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130006"
---
# <a name="prepare-the-input-trace-data"></a>准备输入跟踪数据
  使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分布式重播功能开始分布式重播之前，必须先从分布式重播管理工具启动预处理阶段以准备输入跟踪数据。 在预处理阶段，分布式重播控制器处理跟踪数据并生成一个中间文件：  
  
 ![分布式重播预处理阶段](../../database-engine/media/preprocess.gif "分布式重播预处理阶段")  
  
 有关预处理阶段的详细信息，请参阅 [SQL Server Distributed Replay](sql-server-distributed-replay.md)。  
  
> [!NOTE]  
>  输入跟踪数据必须在与分布式重播兼容的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本中捕获。 输入跟踪数据还必须与要对其重播跟踪数据的目标服务器兼容。 有关版本要求的详细信息，请参阅 [Distributed Replay Requirements](distributed-replay-requirements.md)。  
  
### <a name="to-prepare-the-input-trace-data"></a>准备输入跟踪数据  
  
1.  **（可选）修改预处理配置设置**：若要修改预处理配置设置（例如，是否筛选系统会话或配置最长空闲时间），你必须修改基于 XML 的预处理配置文件 `<PreprocessModifiers>` 的 `DReplay.exe.preprocess.config`元素。 在修改预处理配置文件时，建议您修改副本而非原始文件。 若要修改设置，请执行以下步骤：  
  
    1.  制作默认预处理配置文件 `DReplay.exe.preprocess.config`的副本并重命名此新文件。 默认预处理配置文件位于管理工具安装文件夹。  
  
    2.  在新配置文件中修改预处理配置设置。  
  
    3.  启动预处理阶段（下一步）时，使用 *preprocess* 选项的 **config_file** 参数指定修改过的配置文件的位置。  
  
     有关预处理配置文件的详细信息，请参阅 [配置 Distributed Replay](configure-distributed-replay.md)。  
  
2.  **启动预处理阶段**：若要准备输入跟踪数据，你必须使用 **preprocess** 选项运行管理工具。 有关详细信息，请参阅[预处理选项（Distributed Replay 管理工具）](preprocess-option-distributed-replay-administration-tool.md)。  
  
    1.  打开 Windows 命令提示符实用工具 (`CMD.exe`)，并导航到 Distributed Replay 管理工具的安装位置 (`DReplay.exe`)。  
  
    2.  （可选）如果控制器服务不是在运行管理工具的计算机上运行，则使用 *controller* 参数 **-m**指定控制器。  
  
    3.  使用 *input_trace_file* 参数 **-i**指定输入跟踪文件的位置和名称。  
  
    4.  使用 *controller_working_directory* 参数 **-d**指定中间文件应保存在控制器上的位置。  
  
    5.  （可选）使用 *config_file* 参数 **-c**指定预处理配置文件的位置。 如果您修改了默认预处理配置文件的副本，则使用此参数来指向新的配置文件。  
  
    6.  （可选）使用 *status_interval* 参数 **-f**指定是否希望管理工具以 30 秒之外的其他频率显示状态消息。  
  
     例如，在与控制器服务相同的计算机上为位于 `c:\trace1.trc`中的跟踪文件、位于 `c:\WorkingDir` 中的控制器工作目录以及在默认 30 秒时显示的状态消息启动预处理阶段时，需要使用以下语法： `dreplay preprocess -i c:\trace1.trc -d c:\WorkingDir`  
  
3.  预处理阶段完成后，中间文件将存储在控制器的工作目录中。 若要启动事件重播阶段，必须使用 **replay** 选项运行管理工具。 有关详细信息，请参阅 [重播跟踪数据](replay-trace-data.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 分布式的重播](sql-server-distributed-replay.md)   
 [Distributed 的 Replay 要求](distributed-replay-requirements.md)   
 [管理工具命令行选项&#40;分布式重播实用工具&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [配置 Distributed Replay](configure-distributed-replay.md)  
  
  