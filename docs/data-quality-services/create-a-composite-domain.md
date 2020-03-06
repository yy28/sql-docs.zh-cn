---
title: 创建复合域
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.createcd.f1
- sql13.dqs.dm.cdproperties.f1
ms.assetid: c7f0bd84-a02e-4a81-885d-985e6415c499
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 89c71bd3864fcaa682d3587a54fc2b32c26e5659
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2020
ms.locfileid: "78339745"
---
# <a name="create-a-composite-domain"></a>创建复合域

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 的知识库中创建复合域。 复合域由应用于单个数据字段的一个或多个单一域组成。 有关复合域的详细信息，请参阅[管理复合域](../data-quality-services/managing-a-composite-domain.md)。  
  
 可以通过两种方法创建新的复合域。 第一种方法是在知识发现活动的“映射”步骤期间，当您正在分析数据示例以便将知识添加到新的或现有的知识库中时。 第二种方法是在域管理活动中，当您创建新域（而非更改现有域）时。 为了创建复合域，您必须已至少创建了两个要添加到该复合域中的单一域。 当您创建新的复合域时，只能使用已创建但尚未添加到现有复合域中的那些单一域。 无法将一个单一域添加到多个复合域中，并且一个复合域无法添加到另一个复合域中。  
  
 在创建复合域后，您可以更改复合域的属性，将引用数据服务添加到域中，创建跨域规则，或创建值关系。 为此，在 **“域管理”** 页的 **“域”** 列表中选择复合域，然后选择适当的选项卡。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a>先决条件  
 为了创建复合域，您必须已创建并打开了一个知识库，而且至少创建了两个要添加到复合域中的单一域。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能创建复合域。  
  
##  <a name="ParsingKnowledgeDiscoveryActivity"></a>在知识发现活动中创建复合域  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开知识库”** ，然后选择知识库；或单击 **“新建知识库”** 并输入新知识库的属性。  
  
3.  选择 **“知识发现”** 作为活动，然后单击 **“创建”** 以创建新知识库；或单击 **“打开”** 以打开现有知识库。  
  
4.  在 **“映射”** 页上，指定到数据源的连接。 有关详细信息，请参阅 [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md)。  
  
5.  在 **“映射”** 表中，从某个空行的 **“源列”** 列的下拉列表中选择一个源列。 确保源列包含由两个现有单一域组成的复合域。 如果相应的单一域不存在，请单击 **“创建域”** 图标。  
  
6.  在 **“映射”** 表中，从某个空行的 **“源列”** 列的下拉列表中选择一个源列。 确保源列包含由两个现有单一域表示的复合域的一部分。 如果相应的单一域不存在，请单击 **“创建域”** 图标以创建单一域。 有关详细信息，请参阅 [创建域](../data-quality-services/create-a-domain.md)。  
  
7.  单击 **“创建复合域”** 图标。  
  
##  <a name="DomainManagementActivity"></a>在域管理活动中创建复合域  
  
1.  在 Data Quality Services 客户端主页中，单击 **“打开知识库”** ，然后选择知识库；或单击 **“新建知识库”** 并输入新知识库的属性。  
  
2.  选择 **“域管理”** 作为活动，然后单击 **“创建”** 以创建新知识库；或单击 **“打开”** 以打开现有知识库。  
  
3.  确保复合域所需的两个或多个单一域存在。 否则，请单击 **“创建域”** 图标并创建它们。 有关详细信息，请参阅 [创建域](../data-quality-services/create-a-domain.md)。  
  
4.  在 **“域管理”** 页上，单击域列表上方的 **“创建复合域”** 图标。  
  
5.  输入名称（对知识库唯一）以及说明（最多 256 个字符）。  
  
6.  在 **“域列表”** 中，选择将成为复合域一部分的域，然后单击右箭头将它们移至 **“复合域中的域”** 表中。  
  
7.  单击“确定”。   
  
##  <a name="CompositeDomainProperties"></a>设置复合域属性  
  
1.  在 **“创建复合域”** 对话框中，输入名称（对知识库唯一）以及说明（最多 256 个字符）。  
  
2.  在 **“域列表”** 中，选择将成为复合域一部分的域，然后单击右箭头将它们移至 **“复合域中的域”** 表中。 这是可添加到您创建的复合域中的单一域列表。 只能使用已创建但尚未添加到现有复合域中的那些单一域。 无法将单一域添加到知识库中的多个复合域，并且一个复合域无法添加到另一个复合域中。  
  
3.  单击“高级”。   
  
4.  请为 **“分析方法”** 选择下列选项之一：  
  
    -   **引用数据**：根据引用数据服务（RDS）格式化数据的方式分析字段的值。 Data Quality Services 将复合域中的值发送到 RDS，RDS 根据复合域中的域返回更正和分析后的数据。  
  
    -   按**顺序**：根据复合域中域的顺序分析字段的值。 第一个值将加入第一个域中，第二个值加入第二个域中，依此类推。  
  
    -   **分隔符**：基于在选择 "分隔符" 时显示的单选按钮中选择的分隔符分析该字段的值。 可以是 **“制表符”**、 **“分号”**、 **“逗号”**、 **“空格”** 或 **“其他”**。 如果选择 **“其他”**，则输入将作为分隔符的值。  
  
5.  如果您为分析方法选择了 **“分隔符”** ，还可以选择 **“基于知识的分析”**。 有关详细信息，请参阅 [Knowledge-Based Parsing](#KnowledgeBaseParsing)。  
  
6.  单击 **“完成”** 以完成域管理活动，如 [结束域管理活动](https://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)中所述。  
  
##  <a name="FollowUp"></a>跟进：在创建复合域后  
 在创建复合域后，您可以对域执行其他域管理任务，可以执行知识发现以便向域添加知识，或者可以向域添加匹配策略。 有关详细信息，请参阅[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)、[管理域](../data-quality-services/managing-a-domain.md)或[创建匹配策略](../data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="KnowledgeBaseParsing"></a>基于知识的分析  
 Data Quality Services 使您能够基于知识分析数据，而不仅仅是基于分隔符或顺序。 当复杂源数据映射到复合域并且您未使用引用数据服务时，使用基于知识的分析。 您可以使用基于知识的分析将数据源中的数据分析到相关的单一域。 使用基于知识的分析，DQS 将首先尝试使用知识将复杂数据分析到单一域。 如果可能，它将字符串的组成部分表示为在一个或多个域中，并将字符串分析到其不同的域中。 例如，假设你将“John B. Doe”作为由全名复合域表示的全名字段中的复杂值。 如果 DQS 确定“John”在 First Name 域中，而确定“Doe”在 Last Name 域中，则 DQS 将基于域知识将“B.”添加进去。 添加到 Middle Name 域中。  
  
 仅当您也选择基于分隔符的分析时，才使用基于知识的分析。 基于知识的分析不能代替分隔符分析，但可以增强其功能。 仅当没有知识可让您进行分析时，DQS 才使用分隔符来进行分析。 在某些情况下，DQS 可通过基于知识的分析来确定一些分析，然后确定通过基于分隔符的分析来确定其他分析。  
  
 当复合域由字符串域组成或复合域由不同类型域（int、date、time 等）混合组成时，可以使用基于知识的分析。 如果数据源由不同类型的数据组成，则首先应针对非字符串数据类型进行分析，然后按上面所述基于域知识对剩余数据进行分析。  
  
 当您使用基于知识的分析时，如果源数据中的值少于复合域中的域，则 DQS 将在缺失的域中放入 Null。 如果源数据中的值多于复合域中的域，则 DQS 将向其中一列添加额外的数据。 如果两个或多个域包含相同的值，数据源将被分析为第一个匹配的域。  
  
  
