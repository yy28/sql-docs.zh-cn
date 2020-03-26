---
title: DQS 中的数据事件探查和通知
ms.date: 03/15/2020
ms.prod: sql
ms.reviewer: jroth
ms.technology: data-quality-services
ms.topic: conceptual
author: swinarko
ms.author: sawinark
ms.openlocfilehash: e0bd9585a48ee30368d145c79f8431e922801a9c
ms.sourcegitcommit: c30a2def43c86860aeec69d3e3029f2296544b13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2020
ms.locfileid: "80243397"
---
# <a name="data-profiling-and-notifications-in-data-quality-services-dqs"></a>Data Quality Services （DQS）中的数据事件探查和通知

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]（DQS）是一种数据分析服务。 DQS 从源分析数据，并显示有关 DQS 活动中的数据的统计信息。

## <a name="attributes-goals-benefits"></a>特性、目标、优点

### <a name="attributes-of-dqs"></a>DQS 的属性

DQS 事件探查具有下列属性：

- 提供数据质量的自动测量。
- 已集成到 DQS 知识管理和数据质量项目中。
- 是动态和可调的。

### <a name="goals-of-dqs"></a>DQS 目标

DQS 分析具有以下两个主要目标：

- 指导您完成数据质量过程和支持您的决策。
- 评估进程的有效性。

### <a name="benefits-of-dqs"></a>DQS 的优点

DQS 分析具有以下优势：

- 提供源数据的质量见解，并帮助您确定数据质量问题。

- 评估数据质量过程，并指导您：
  - 知识发现
  - 数据清理
  - 匹配策略
  - 匹配工作

- 在最相关的时间提供最相关的信息。

- 生成强调重要统计信息或可能保证操作的事件的通知。 DQS 通知通常指示条件，并建议纠正措施。

DQS 事件探查提供知识发现、数据清理和数据匹配。 DQS 也是数据分析工具。 您可以创建用于分析的知识库。 然后，可以使用知识库运行知识发现。 知识发现使用分析统计信息来确定知识库是否满足发现、清理和匹配的需要。

## <a name="how-dqs-profiling-works"></a><a name="How"></a>DQS 事件探查的工作原理

DQS 事件探查不衡量知识库的质量。 分析度量源数据的质量。 事件探查提供的统计信息指示以下工作的效果：

- 知识管理中的特定操作。
- 源数据上的数据质量项目。

### <a name="activity-context"></a>活动上下文

事件探查始终处于您正在执行的特定活动的上下文中。 您可以单击屏幕中的 "事件探查" 选项卡以显示分析数据。 此单击不会将你转到你正在执行的活动的阶段。 执行该过程时，将实时填充分析表。 因此，您可以在执行数据质量任务时对其进行评估。

您可以确定源数据在清除或消除重复数据后是否更好以及改善的程度。

### <a name="profiling-is-based-on-counts"></a>分析基于计数

所有事件探查号都是指特定值的外观计数。 在许多情况下，数字是指总计的百分比。 唯一性度量值是一个例外。 唯一性指标指的是值的绝对值，而不考虑这些值的外观计数。

### <a name="knowledge-driven-solution"></a>知识驱动的解决方案

数据探查是 DQS 知识驱动解决方案的一部分。 分析提供有关知识库、匹配或数据清除过程的信息。 此信息基于数据源字段与知识库域之间的映射。 仅在完成映射后才执行事件探查。 任何活动的映射阶段都不会执行分析。

事件探查始终与活动关联。 分析过程是针对_映射_到域的数据（而不是域_中_的数据）执行的。

事件探查已集成到活动的以下步骤中：

- 知识发现活动的 "**发现**" 和 "**管理域值**" 步骤。

- 清理活动的 "**清理**" 和 "**管理和查看结果**" 步骤。

- 匹配策略活动的 "**匹配策略**" 和 "**匹配结果**" 步骤。

- 匹配活动的**匹配**和**导出**步骤。

DQS 不为“域管理”活动提供事件探查的统计信息。

## <a name="profiling-data-by-activity"></a><a name="Activity"></a>按活动分析数据

DQS 事件探查使用以下标准数据质量维度来表示数据的质量：

- 完整性-数据的存在程度。
- 准确性-数据可用于其预期用途的程度。
- 唯一性-不同值表示不同实体的程度。

默认情况下，NULL 值和空值被视为缺失，或者降低完整性百分比。 但是，可以将其他值定义为与 NULL 等效。 这些值也被视为缺失。

事件探查为您提供评估您的过程所需的统计信息，但您必须解释这些统计信息。 通过逐列查看统计信息，可以了解事件探查可为您提供什么信息。

### <a name="differing-sets-of-profiling-statistics"></a>不同的分析统计信息集

DQS 活动具有不同的事件探查统计信息集，如下所示：

- 只有清理活动具有准确性事件探查统计信息（按域以百分比表示）。 有效性、一致性、语法错误和域规则都会影响准确性。

- 只有清理活动对源中正确、已更正、建议的值以及按域更正和建议的值（均为百分比数字）提供事件探查统计信息。

- 清理和知识发现活动具有有效性事件探查统计信息（按记录清理、按记录和域进行知识发现）。 匹配策略和匹配活动没有有效性统计信息。

- 为源和域提供的事件探查统计信息是唯一的。 此语句适用于以下活动：
  - 知识发现。
  - 匹配策略。
  - 一致.
  - 但_不能_用于清理活动。

DQS 提供与活动相关的特定事件探查统计信息。 有关详细信息，请参阅以下主题中的**分析**部分：

- [执行知识发现](../data-quality-services/perform-knowledge-discovery.md)

- [使用 DQS &#40;内部&#41; 知识清理数据](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [创建匹配策略](../data-quality-services/create-a-matching-policy.md)

- [运行匹配项目](../data-quality-services/run-a-matching-project.md)

## <a name="profiling-data-in-activity-monitoring"></a><a name="Monitoring"></a>活动监视中的事件探查数据

事件探查信息不仅可用于数据质量客户端的活动页，也可用于活动监视。 信息涉及知识发现、匹配策略、匹配和清理活动。 该信息在数据质量客户端和活动监视中的活动页中提供。

你可以在一个位置查看所有以下项：

- 属性
- 相关的活动计算过程
- 为每个活动生成的分析信息

您可以在活动表中选择一个活动，以便在第二个表中显示事件探查结果。 此外，还可以导出事件探查结果。

有关详细信息，请参阅 [DQS Administration](../data-quality-services/dqs-administration.md)。

## <a name="notifications"></a><a name="Notifications"></a>报警

DQS 会生成通知，以指示何时可能需要根据所分析的统计信息执行操作。 DQS 使用有关数据源的重要事实的通知。 这些事实显示当前活动相对于其执行目的的有效性。 通知提供指示条件的提示和建议。 通知还可能会建议您如何改进知识发现、数据清理或数据匹配活动。

DQS 在检测到可能对你很重要的问题时发送通知。 例如，当完整性和准确性均为100% 时，数据清理活动可能不会生成任何更正或建议的值。 DQS 可能会在这种情况下发布通知。 此通知将表明可能不需要此活动。 是否运行活动仍可决定。

通知由带有感叹号的工具提示指示，在 "**分析**" 选项卡中。与通知关联的统计信息为红色，以指示通知的统计理由。

### <a name="disable-notifications"></a>禁用通知

默认情况下启用通知。 但你可以通过使用 Data Quality Client 主页来禁用通知。 在 "**管理**" 部分中，使用 "**常规设置**" 选项卡。

禁用通知时，不会显示工具提示，并且统计信息不会显示为红色。 禁用通知时，分析仍可正常运行。 禁用通知不会提高性能。

有关与活动通知相关联的特定条件，请参阅下列资源：

- [执行知识发现](../data-quality-services/perform-knowledge-discovery.md)

- [使用 DQS &#40;内部&#41; 知识清理数据](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [创建匹配策略](../data-quality-services/create-a-matching-policy.md)

- [运行匹配项目](../data-quality-services/run-a-matching-project.md)

## <a name="related-tasks"></a>Related Tasks

| 任务说明 | 主题 |
| :--------------- | :---- |
| 说明如何在 DQS 中启用或禁用通知。 | [在 DQS 中启用或禁用事件探查通知](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md) |
|||
