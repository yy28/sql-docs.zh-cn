---
title: "CDC 源编辑器 （连接管理器页） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.cdcsource.connection.f1
ms.assetid: 304e6717-e160-4a7b-a06f-32182449fef8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 45b89dbd00ad63610c967887c0c8a166d977e958
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="cdc-source-editor-connection-manager-page"></a>CDC 源编辑器（“连接管理器”页）
  可以使用“CDC 源编辑器”对话框的“连接管理器”页，为 CDC 源从其中读取更改行的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 数据库（CDC 数据库）选择 ADO.NET 连接管理器。 一旦选择了 CDC 数据库，则需要选择该数据库中的一个捕获表。  
  
 有关 CDC 源的详细信息，请参阅 [CDC Source](../../integration-services/data-flow/cdc-source.md)。  
  
## <a name="task-list"></a>任务列表  
 **打开“CDC 源编辑器”的“连接管理器”页**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开具有 CDC 源的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 CDC 源。  
  
3.  在 **“CDC 源编辑器”**中，单击 **“连接管理器”**。  
  
## <a name="options"></a>选项  
 **ADO.NET 连接管理器**  
 从列表中选择现有连接管理器，或单击“新建”创建新的连接。 该连接必须是指向为 CDC 启用的并且所选更改表位于其中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接。  
  
 **新建**  
 单击 **“新建”**。 **“配置 ADO.NET 连接管理器编辑器”** 对话框打开，可在其中创建新的连接管理器。  
  
 **CDC 表**  
 选择您要读取并馈送到下游 SSIS 组件以便处理的捕获更改所在的 CDC 源表。  
  
 **捕获实例**  
 选择或键入具有要读取的 CDC 表的“CDC 捕获实例”的名称。  
  
 一个捕获源表可具有一个或两个捕获实例，以便通过架构更改处理表定义的无缝转换。 如果为要捕获的源表定义了一个捕获实例，则选择要在此处使用的捕获实例。 表 [架构] 默认捕获实例名称。[表] 是\<架构 > _\<表 >，但在使用实际的捕获实例名称可能不同。 从读取的实际表是 CDC 表**cdc。\<捕获实例 > _CT**。  
  
 **CDC 处理模式**  
 选择可以最好地满足您的处理需要的处理模式。 可能的选项包括：  
  
-   **所有**：返回当前 CDC 范围中的更改，但没有 **“更新前”** 值。  
  
-   **全部且具有旧值**：返回当前 CDC 处理范围中的更改，包括旧值（“更新前”）。 对于每个更新操作将会有两行，一个针对更新前值，一个针对更新后值。  
  
-   **净值**：对于当前 CDC 处理范围中修改的每个源行，仅返回一个更改行。 如果某一源行更新了多次，将生成合并的更改（例如，插入+更新作为单个更新生成，更新+删除作为单个删除生成）。 在净更改处理模式下工作时，可以拆分对删除、插入和更新输出的更改并且并行处理它们，因为单个源行出现多次。  
  
-   **具有更新掩码的净值**： 这种模式十分类似于常规 Net 模式，但它还添加了具有名称模式的布尔值列**__ $\<列名称 >\__Changed** ，可指示在当前已更改的列更改行。  
  
-   **净值且具有合并**：此模式类似于一般的净值模式，但具有合并到单个合并操作中的插入和更新操作 (UPSERT)。  
  
> [!NOTE]  
>  对于所有净更改选项，源表必须具有主键或唯一索引。 对于不具有主键或唯一索引的表，您必须选择 **“全部”** 选项。  
  
 **包含 CDC 状态的变量**  
 选择为当前 CDC 上下文维护 CDC 状态的 SSIS 字符串包变量。 有关 CDC 状态变量的详细信息，请参阅[定义状态变量](../../integration-services/data-flow/define-a-state-variable.md)。  
  
 **包括重新处理指示器列**  
 选中此复选框可以创建称作 **__$reprocessing**的特殊输出列。  
  
 在 CDC 处理范围与初始处理范围（与初始加载期间相对应的 LSN 的范围）重叠时，或者在之前的运行存在错误后重新处理某一 CDC 处理范围时，该列具有值 **true** 。 通过此指示器列，SSIS 开发人员可以在重新处理更改时以不同方式处理错误（例如，可忽略删除不存在的行和插入在重复键上失败之类的操作）。  
  
 有关详细信息，请参阅 [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CDC 源编辑器 &#40;列页 &#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)   
 [CDC 源编辑器 &#40;错误输出页 &#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  
