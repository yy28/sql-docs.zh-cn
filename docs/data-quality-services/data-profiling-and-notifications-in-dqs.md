---
title: DQS 中的数据事件探查和通知
ms.date: 04/01/2020
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a778bb5b-8e35-4a7b-b04a-ae2b46dec21b
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 1e5c51996ba85b9645650f453a0e4ed18478ccf7
ms.sourcegitcommit: 52925f1928205af15dcaaf765346901e438ccc25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2020
ms.locfileid: "80607825"
---
# <a name="data-profiling-and-notifications-in-dqs"></a>DQS 中的数据事件探查和通知

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的数据事件探查是一个分析现有数据源中的数据并显示有关 DQS 活动中的数据统计信息的过程。 它为您提供了数据质量的自动测量。 DQS 事件探查已集成到 DQS 知识管理和数据质量项目中。 它是动态的，可调的。 事件探查具有两个主要目的：第一，引导您完成数据质量过程和支持您做出决策；第二，评估过程的效用。 DQS 事件探查具有下列优点：  
  
-   事件探查可让您深入了解源数据的质量，并帮助您确定数据质量问题。  
  
-   事件探查可评估数据质量过程的效用，同时指导您进行知识发现、数据清理、匹配策略和匹配工作。  
  
-   事件探查在最合适的时间向您展示最相关的信息。  
  
-   分析过程生成通知，强调重要统计信息或可能需要执行操作的事件。 在许多情况下，DQS 通知指示一种条件，并建议您采取措施来进行补救。  
  
 通过事件探查，您不仅可以使用 Data Quality Services 来进行知识发现、清理和匹配，还可以用作分析工具。 您可能需要创建一个知识库来进行分析，并使用该知识库来运行知识发现，以便通过事件探查统计信息来确定知识库是否满足发现、清理和匹配的需要。  
  
##  <a name="how-profiling-works"></a><a name="How"></a> 事件探查的工作原理  
 分析不衡量知识库的质量。 它衡量源数据的质量。 分析为您提供统计信息，用于指示您在知识管理或数据质量项目中执行的特定操作对源数据的影响。 分析始终位于您正在执行的特定活动的上下文中。 您可以单击屏幕中的分析选项卡以显示分析数据，而无需离开正在执行的操作阶段。 执行该过程时实时填充分析表，使您能够在执行任务时评估数据质量任务。 您可以确定源数据在清除或消除重复数据后是否更好以及改善的程度。  
  
 所有分析编号都指值的外观数，在许多情况下引用总数的百分比，唯一性指标除外。 唯一性度量指标指的是值的绝对数字，而不考虑这些值的出现次数。  
  
 数据探查是 DQS 知识驱动解决方案的一部分。 它根据数据源字段与知识库域之间的映射提供有关知识库、匹配或数据清除过程的信息。 仅在映射完成后进行配置文件;在任何活动的映射阶段不执行任何分析。 事件探查始终与活动关联。 分析过程对映射到域的数据执行，而不是对域中的数据执行。 它集成到以下活动步骤中：  
  
-   知识发现活动的 **“发现”** 和 **“管理域值”** 步骤  
  
-   清理活动的 **“清理”** 和 **“管理和查看结果”** 步骤  
  
-   匹配策略活动的 **“匹配策略”** 和 **“匹配结果”** 步骤  
  
-   匹配活动的 **“匹配”** 和 **“导出”** 步骤  
  
 DQS 不提供域管理活动的分析统计信息。  
  
##  <a name="profiling-data-by-activity"></a><a name="Activity"></a> 按活动的事件探查数据  
 DQS 事件探查使用标准数据质量维度来表示数据的质量：完整性（提供数据的范围）、准确性（数据可用于目标用途的程度）以及唯一性（不同值表示不同实体的程度）。 默认情况下，NULL 和空值被视为缺失，或降低完整性百分比;但是，您还可以将其他值定义为 NULL 等效值，在这种情况下，它们也将被视为缺失。  
  
 事件探查为您提供评估您的过程所需的统计信息，但您必须解释这些统计信息。 通过逐列查看统计信息，可以了解事件探查可为您提供什么信息。  
  
 DQS 活动具有不同的事件探查统计信息集，如下所示：  
  
-   只有清理活动具有准确性事件探查统计信息（按域以百分比表示）。 有效性、一致性、语法错误和域规则都会影响准确性。  
  
-   只有清理活动对源中正确、已更正、建议的值以及按域更正和建议的值（均为百分比数字）提供事件探查统计信息。  
  
-   清理和知识发现活动具有有效性事件探查统计信息（按记录清理、按记录和域进行知识发现）。 匹配策略和匹配活动没有有效性统计信息。  
  
-   清理活动没有唯一性的分析统计信息。 知识发现、匹配策略和匹配活动具有唯一性事件探查统计信息（按域以源的数字和百分比来表示）。  
  
 有关与活动相关的特定分析统计信息的详细信息，请参阅以下文章中的"分析"部分：  
  
-   [执行知识发现](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [使用 DQS（内部）知识清理数据](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [创建匹配策略](../data-quality-services/create-a-matching-policy.md)  
  
-   [运行匹配项目](../data-quality-services/run-a-matching-project.md)  
  
##  <a name="profiling-data-in-activity-monitoring"></a><a name="Monitoring"></a>在活动监视中分析数据  
 知识发现、匹配策略、匹配和清理活动的分析信息不仅在数据质量客户端的活动页中可用，而且在活动监视中也可用。 活动监视向您提供当前和过去活动的概述。 除了活动的属性和相关的计算过程之外，您还可以查看针对一个位置的每个活动生成的事件探查信息。 您可以在活动表中选择一个活动，以便在下表中显示事件探查结果。 此外，还可以导出事件探查结果。 有关详细信息，请参阅 [DQS Administration](../data-quality-services/dqs-administration.md)。  
  
##  <a name="notifications"></a><a name="Notifications"></a>通知  
 除了通过事件探查收集和显示重要统计信息和度量指标之外，DQS 还将生成通知（如果已启用），以指示您根据所显示的事件探查统计信息，何时可能需要采取措施。 DQS 使用通知来强调有关数据源的重要事实，并显示当前活动与执行目的相比的有效性。 通知提供相关的提示和建议，这些信息指示某种条件并建议您如何改进知识发现、数据清除或数据匹配活动。  
  
 DQS 通知用于提出您可能感兴趣的问题或解决潜在的问题。 您是否对通知采取行动取决于该通知是否与您的目的相关。 例如，假设当完整性和准确性均为 100% 时，如果数据清理没有生成任何更正值或建议值，则 DQS 会发布一个通知。 此通知将表明可能不需要运行该活动。 是否选择运行此活动取决于您。  
  
 通知由"**分析"** 选项卡中带有感叹号的工具提示指示。与通知关联的统计信息为红色，以指示通知的统计理由。  
  
 您可以在数据质量客户端主页中 **“管理”** 部分的 **“常规设置”** 选项卡上启用（默认）或禁用通知。 禁用通知后，不会显示工具提示，统计信息不会显示为红色。 禁用通知没有显著改善性能。 如果您禁用通知，事件探查仍会进行。  
  
 有关与活动通知关联的特定条件，请参阅以下文章：  
  
-   [执行知识发现](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [使用 DQS（内部）知识清理数据](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [创建匹配策略](../data-quality-services/create-a-matching-policy.md)  
  
-   [运行匹配项目](../data-quality-services/run-a-matching-project.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|项目|  
|----------------------|-----------|  
|说明如何在 DQS 中启用或禁用通知。|[在 DQS 中启用或禁用事件探查通知](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
  
  
