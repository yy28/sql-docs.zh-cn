---
description: 创建基于字词的关系
title: 创建基于字词的关系
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.kbtermsbased.f1
ms.assetid: 66db9277-d892-4dae-8a82-060fd3ba6949
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 0dfc837238d20e58b04b66ae4ea998e60ee80247
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725365"
---
# <a name="create-term-based-relations"></a>创建基于字词的关系

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  本主题描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中为域创建基于字词的关系。 通过基于字词的关系 (TBR)，您可以对域中作为值的一部分的字词进行更正。 基于字词的关系使完全相同的多个值（只有其公共部分的拼写除外）可被视为相同的同义词。 例如，可以设置一个基于字词的关系，该关系可将字词“Inc.” 更改为“Incorporated”。 字词“Inc.” 将在其每次出现在域中时发生更改。 “Contoso, Inc.”的实例 将更改为“Contoso, Incorporated”，并且这两个值将被视为精确同义词。  
  
 若要使用基于字词的关系，可以生成一个“值/更正为”对的列表，例如“Inc.” 和“Incorporated”或“Senior”和“Sr.”。 通过使用基于字词的关系，您可以在整个域中更改某一字词，而不必手动将单独的域值设置为同义词。 您也可以指定更正某个值，即使知识发现以前尚未发现该值。 如果基于字词的关系转换导致两个值完全相同，则 DQS 将在它们之间创建一个同义词关系（在知识发现中）、更正关系（在数据更正中）或精确匹配（在匹配中）。  
  
 基于字词的关系转换和符号转换（其中，特殊字符将被空格或 null 替换）都在分析前的预处理阶段中完成。 如果请求复合域分析，将在这两个转换前执行分析，因为分隔符分析要求符号。 其他操作（例如域规则和域值更改）将会在转换后执行。 对于匹配，在匹配活动前，将基于字词的关系应用于源数据，而与您是否运行清理无关。  
  
 **基于字词的关系和域管理**  
  
 在域管理中应用基于字词的关系时，DQS 将应用知识发现、清理或匹配过程中的更改；但是，DQS 不更改域值本身以便遵从基于字词的关系。 换句话说，如果在 **“域管理”** 页的 **“基于字词的关系”** 选项卡上输入并接受一个基于字词的关系，该更改不会在同一页的 **“域值”** 选项卡中执行。 这使您可以随后更改 TBR。  
  
 **基于字词的关系和数据清理**  
  
 在域中应用基于字词的关系并运行数据清理过程时，DQS 将在清理过程中应用更改，但是这些更改不会应用于知识库中的字词。  
  
-   如果基于字词的关系所更改的值在域中但不是同义词，它将显示在 **“更正为”** 列（位于 **“管理和查看结果”** 页的 **“已更正”** 选项卡下）中，且将“原因”设置为“基于字词的关系”。  
  
-   如果基于字词的关系所更改的值不在域中且 DQS 找到了匹配值，则该值将更改为它且显示在“已更正”选项卡或“建议的”选项卡下（具体取决于置信度级别）。 如果找不到匹配值，该值将显示在“新建”下并带一个 TBR 更正项。 这么做是因为即使您更正了 TBR，也不表示该值是正确的。  
  
-   如果基于字词的关系所更改的值在域中但值错误/无效且已有更正项，则该值将显示在“已更正”选项卡下且具有更正项和原因“域值”。  
  
-   如果基于字词的关系所更改的值在域中但值错误/无效且无更正项，则该值将显示在“无效”选项卡下且具有原因“域值”。  
  
 **基于字词的关系和知识发现**  
  
 当您应用基于字词的关系，然后运行知识发现过程时，符合 TBR 的所有值将保持原样并被标识为正确值。 TBR 所更改的所有值将被导入为正确值并被标识为符合 TBR 的值的同义词。  
  
 **基于字词的关系和将清理值导入域**  
  
 如果您将在清理过程中收集的数据质量知识导入到域中，TBR 所更改的值将作为正确值导入。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
 若要创建基于字词的关系，您必须具有在域管理活动中打开的知识库。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能创建基于字词的关系。  
  
##  <a name="create-term-based-relations"></a><a name="Create"></a> 创建基于字词的关系  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的主屏幕中，打开或创建一个知识库。 选择 **“域管理”** 作为活动，然后单击 **“打开”** 或 **“创建”**。 有关详细信息，请参阅 [创建知识库](../data-quality-services/create-a-knowledge-base.md) 或 [打开知识库](../data-quality-services/open-a-knowledge-base.md)。  
  
    > [!NOTE]  
    >  域管理在 Data Quality Service 客户端页面中执行，该页面包含用于单独域管理操作的五个选项卡。 它不是一个向导驱动的过程；任何管理操作都可以单独执行。  
  
3.  从 **“域管理”** 页上的 **“域列表”** 中，选择您要为其创建域规则的域，或者创建一个新的域。 如果您必须创建新域，请参阅 [创建域](../data-quality-services/create-a-domain.md)。  
  
4.  单击 **“基于字词的关系”** 选项卡。  
  
5.  按如下所示创建基于字词的关系：  
  
    1.  单击 **“添加新关系”** 可将行添加到“关系”表。  
  
    2.  对于添加的行的 **“值”** 列，输入每次在所选域的值中出现时将要更改的字词。  
  
        > [!NOTE]  
        >  如果该字词在域中作为整个值存在，或者已在域中作为更正值存在，系统将会向您显示一个错误消息。  
  
    3.  对于 **“更正为”** 列，输入您要将 **“值”** 列中的字词更改为的字词。  
  
    4.  再次单击 **“添加新关系”** 可添加另一个基于字词的关系。  
  
    5.  单击 **“删除所选关系”** 可从“关系”表中删除一个或多个选定的行。 通过按下 Ctrl 键并单击未选定的行，可以选择多个行。  
  
    6.  通过在 **“查找”** 文本框中输入一个或多个数字，可以在“关系”表中查找一个值。 该字符串的匹配项将会突出显示。 使用向上箭头和向下箭头可以移到表中该字符串的不同实例。  
  
    7.  **拼写检查器**：如果 **“值”** 或 **“更正为”** 列中的值有红色的波浪下划线，则表示拼写检查器建议对该值加以更正。 右键单击带下划线的值，然后选择由拼写检查器提供的建议值之一。 或者，您可以单击快捷菜单中的 **“添加”** ，以继续使用原始值。 有关详细信息，请参阅 [使用 DQS 拼写检查器](../data-quality-services/use-the-dqs-speller.md) 和 [设置域属性](../data-quality-services/set-domain-properties.md)。  
  
        > [!NOTE]  
        >  若要使用拼写检查器，您或者可以在 **“域属性”** 页中启用它，或者如果已在 **“域属性”** 页中禁用它，则可以在 **“基于字词的关系”** 页中单击 **“启用/禁用拼写检查器”** 图标以便在该页上启用它。  
  
6.  单击 **“应用更改”** 可将基于字词的关系应用于域。  
  
7.  单击 **“完成”** 以完成域管理活动，如 [结束域管理活动](/previous-versions/sql/sql-server-2016/hh510411(v=sql.130))中所述。  
  
##  <a name="follow-up-after-creating-term-based-relations"></a><a name="FollowUp"></a> 跟进：在创建基于字词的关系后  
 在创建基于字词的关系后，您可以对域执行其他域管理任务，可以执行知识发现以便向域添加知识，或者可以向域添加匹配策略。 有关详细信息，请参阅[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)、[管理域](../data-quality-services/managing-a-domain.md)或[创建匹配策略](../data-quality-services/create-a-matching-policy.md)。  
  
