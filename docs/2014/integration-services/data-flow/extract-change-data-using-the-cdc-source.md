---
title: 使用 CDC 源提取更改数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 604fbafb-15fa-4d11-8487-77d7b626eed8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e0e4fe1f3c7920f034103a4fca6df3460ff4aea7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915777"
---
# <a name="extract-change-data-using-the-cdc-source"></a>使用 CDC 源提取更改数据
  若要添加并配置 CDC 源，则包必须已包含至少一个数据流任务和一个 CDC 控制任务。  
  
 有关 CDC 控制任务的详细信息，请参阅 [CDC Control Task](../control-flow/cdc-control-task.md)。  
  
 有关 CDC 源的详细信息，请参阅 [CDC Source](cdc-source.md)。  
  
### <a name="to-extract-change-data-using-a-cdc-source"></a>使用 CDC 源提取更改数据  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开包含所需包的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，然后从 **“工具箱”** 把 CDC 源拖动到设计图面。  
  
4.  双击此 CDC 源。  
  
5.  在 **“CDC 源编辑器”** 对话框中的 **“连接管理器”** 页上，从列表中选择现有的 ADO.NET 连接管理器，或单击 **“新建”** 创建新的连接。 该连接应该是与包含要读取的更改表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接。  
  
6.  选择要处理更改的 **“CDC 表”** 。  
  
7.  选择或键入具有要读取的 CDC 表的 **“CDC 捕获实例”** 的名称。  
  
     一个捕获源表可具有一个或两个捕获实例，以便通过架构更改处理表定义的无缝转换。 如果为要捕获的源表定义了一个捕获实例，则选择要在此处使用的捕获实例。 表 [schema] 的默认捕获实例名称。[表] 为 \<schema> _ \<table> ，但使用的实际捕获实例名称可能不同。 从中读取的实际表是 CDC 表**cdc。 \<capture-instance>_CT**。  
  
8.  选择可以最好地满足您的处理需要的处理模式。 可能的选项包括：  
  
    -   **所有**：返回当前 CDC 范围中的更改，但没有 **“更新前”** 值。  
  
    -   **全部且具有旧值**：返回当前 CDC 处理范围中的更改，包括旧值（“更新前”  ）。 对于每个更新操作将会有两行，一个针对更新前值，一个针对更新后值。  
  
    -   **净值**：对于当前 CDC 处理范围中修改的每个源行，仅返回一个更改行。 如果某一源行更新了多次，将生成合并的更改（例如，插入+更新作为单个更新生成，更新+删除作为单个删除生成）。 在净更改处理模式下工作时，可以拆分对删除、插入和更新输出的更改并且并行处理它们，因为单个源行出现多次。  
  
    -   **Net with 更新掩码**：此模式类似于常规 Net 模式，但它还添加了命名模式为 **__ $ \<column-name> \_ _Changed**的布尔值列，用于指示当前更改行中已更改的列。  
  
    -   **净值且具有合并**：此模式类似于一般的净值模式，但具有合并到单个合并操作中的插入和更新操作 (UPSERT)。  
  
9. 选择为当前 CDC 上下文维护 CDC 状态的 SSIS 字符串包变量。 有关 CDC 状态变量的详细信息，请参阅 [定义状态变量](define-a-state-variable.md)。  
  
10. 选中“包括重新处理指示器列”  复选框可以创建称作 **__$reprocessing** 的特殊输出列。 在 CDC 处理范围与初始处理范围（与初始加载期间相对应的 LSN 的范围）重叠时，或者在之前的运行存在错误后重新处理某一 CDC 处理范围时，该列具有值 **true** 。 通过此指示器列，SSIS 开发人员可以在重新处理更改时以不同方式处理错误（例如，可忽略删除不存在的行和插入在重复键上失败之类的操作）。  
  
     有关详细信息，请参阅 [CDC Source Custom Properties](cdc-source-custom-properties.md)。  
  
11. 若要更新外部列和输出列之间的映射，请单击 **“列”** ，并在 **“外部列”** 列表中选择其他列。  
  
12. 也可以通过删除 **“输出列”** 列表中的值来更新输出列的值。  
  
13. 若要配置错误输出，请单击 **“错误输出”** 。  
  
14. 可以单击 **“预览”** ，查看最多 200 行 CDC 源所提取的数据。  
  
15. 单击“确定”。   
  
## <a name="see-also"></a>另请参阅  
 [CDC 源编辑器（“连接管理器”页）](../cdc-source-editor-connection-manager-page.md)   
 [CDC 源编辑器（“列”页）](../cdc-source-editor-columns-page.md)   
 [CDC 源编辑器（“错误输出”页）](../cdc-source-editor-error-output-page.md)  
  
  
