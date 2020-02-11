---
title: 使用检查点重启包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 48f2fbb7-8964-484a-8311-5126cf594bfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1f41ed858bedd18ec68794d5e7d1c13100af5254
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767029"
---
# <a name="restart-packages-by-using-checkpoints"></a>通过使用检查点重新启动包
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可以从失败点重新启动失败的包，而不是重新运行整个包。 如果包配置为使用检查点，则关于包执行的信息会写入检查点文件中。 当重新运行失败的包时，可以使用检查点文件从失败点重新启动该包。 如果包成功运行，则会删除该检查点文件，然后在下次运行包时会重新创建相应的检查点文件。  
  
 在包中使用检查点可以提供下列好处：  
  
-   避免重复下载和上载大型文件。 例如，对于每次下载都使用 FTP 任务下载多个大型文件的包，如果下载单个文件失败，则可以重新启动该包，只下载该失败的文件。  
  
-   避免重复加载大量数据。 例如，对于为每个维度使用不同的大容量插入任务向数据仓库中的维度表执行大容量插入的包，如果某一维度表的插入失败，则可以重新启动该包，只重新加载该失败的维度。  
  
-   避免重复聚合值。 例如，如果包需要计算多个聚合，例如求平均值和求和，而且使用不同的数据流任务执行每个聚合，则在计算一个聚合失败时，可以重新启动该包，只重新计算该失败的聚合。  
  
 如果包配置为使用检查点， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将捕获检查点文件中的重新启动点。 失败的容器类型以及功能（例如事务）的实现都会影响在检查点文件中所记录的重新启动点。 检查点文件中还捕获变量的当前值。 但是，数据类型为 `Object` 的变量的值不保存在检查点文件中。  
  
## <a name="defining-restart-points"></a>定义重新启动点  
 封装单个任务的任务宿主容器是可以重新启动的最小原子工作单元。 Foreach 循环容器和事务处理容器也被视为原子工作单元。  
  
 如果在事务处理容器运行时停止某个包，则该事务将会结束，并且将回滚该容器执行的所有工作。 当重新启动该包时，会重新运行失败的容器。 检查点文件中不记录事务处理容器的任何子容器的完成情况。 因此，当重新启动包时，会再次运行事务处理容器及其子容器。  
  
> [!NOTE]  
>  在同一个包中使用检查点和事务可能会导致意外的结果。 例如，当包失败并从某个检查点重新启动时，该包可能会重复已成功提交的事务。  
  
 不为 For 循环和 Foreach 循环容器保存检查点数据。 当重新启动包时，会再次运行 For 循环和 Foreach 循环容器及其子容器。 如果循环中的子容器已成功运行，则不会将其记录在检查点文件中，而是重新运行子容器。 有关解决方法的详细信息，请参阅 [不为 For 循环和 Foreach 循环容器项采用 SSIS 检查点](https://go.microsoft.com/fwlink/?LinkId=241633)。  
  
 在重新启动包时，不会重新加载包配置，包使用写入检查点文件中的配置信息。 这就确保包在重新运行时使用的是与失败时相同的配置。  
  
 包只能在控制流级重新启动。 您无法重新启动处于数据流中间的包。 为了避免重新运行整个数据流，可以将包设计为包括多个数据流，每个数据流使用不同的数据流任务。 这样，在重新启动包时，将只需重新运行一个数据流任务。  
  
## <a name="configuring-a-package-to-restart"></a>将包配置为重新启动  
 检查点文件包括所有已完成的容器的执行结果、系统变量和用户定义的变量的当前值以及包配置信息。 该文件还包括包的唯一标识符。 若要成功重新启动包，检查点文件中的包标识符和包必须匹配，否则重新启动将失败。 这样可以防止包使用其他包版本所写的检查点文件。 如果包成功运行，则在包重新启动后，将会删除该检查点文件。  
  
 下表列出了可设置为实现检查点的包属性。  
  
|properties|说明|  
|--------------|-----------------|  
|CheckpointFileName|指定检查点文件的名称。|  
|CheckpointUsage|指定是否使用检查点。|  
|SaveCheckpoints|指示包是否保存检查点。 此属性必须设置为 True，才能从失败点重新启动包。|  
  
 此外，对于包中要标识为重新`true`启动点的所有容器，必须将 FailPackageOnFailure 属性设置为。  
  
 可以使用 ForceExecutionResult 属性测试包中检查点的使用情况。 通过将容器或任务的 ForceExecutionResult 设置为 Failure，可以模拟实时的失败。 当重新运行包时，将重新运行失败的任务和容器。  
  
### <a name="checkpoint-usage"></a>检查点用法  
 CheckpointUsage 属性可设置为下列值：  
  
|值|说明|  
|-----------|-----------------|  
|`Never`|指定不使用检查点文件，包从包工作流的起点开始运行。|  
|`Always`|指定始终使用检查点文件，包从上一次执行失败的点重新启动。 如果找不到检查点文件，则包失败。|  
|`IfExists`|指定如果存在检查点文件则使用该文件。 如果检查点文件存在，则包从上一次执行失败的点重新启动；如果检查点文件不存在，则包从包工作流的起点开始运行。|  
  
> [!NOTE]  
>  Dtexec 的 **/checkpointing on on**选项等效于将包的`SaveCheckpoints`属性设置为`True`，并将属性设置为`CheckpointUsage` "始终"。 有关详细信息，请参阅 [dtexec Utility](dtexec-utility.md)。  
  
## <a name="securing-checkpoint-files"></a>保护检查点文件  
 包级别的保护不包括保护检查点文件，必须单独保护这些文件。 检查点数据只能存储在文件系统中，应当使用操作系统访问控制列表 (ACL) 来保护用于存储该文件的位置或文件夹。 重要的是务必保护检查点文件，因为它们包含了有关包状态的信息，包括变量的当前值。 例如，变量可能包含由很多行私人数据（如电话号码）组成的记录集。 有关详细信息，请参阅[访问包使用的文件](../access-to-files-used-by-packages.md)。  
  
### <a name="to-configure-the-checkpoint-properties"></a>配置检查点属性  
  
-   [配置检查点以重新启动失败的包](../configure-checkpoints-for-restarting-a-failed-package.md)  
  
## <a name="external-resources"></a>外部资源  
  
-   social.technet.microsoft.com 上的技术文章： [在故障转移或失败后自动重新启动 SSIS 包](https://go.microsoft.com/fwlink/?LinkId=200407)  
  
-   support.microsoft.com 上的支持文章： [不为 For 循环和 Foreach 循环容器项采用 SSIS 检查点](https://go.microsoft.com/fwlink/?LinkId=241633)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
