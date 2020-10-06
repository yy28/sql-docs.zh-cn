---
description: 设置域属性
title: 设置域属性
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.domainproperties.f1
ms.assetid: 8a3c88ca-31d6-4f75-9aca-cf027c6d9845
author: swinarko
ms.author: sawinark
ms.openlocfilehash: a229aacb9110bdd5eefa9dc3987ce39fec8a1e66
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726601"
---
# <a name="set-domain-properties"></a>设置域属性

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中设置域属性。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
 若要为域设置属性，您必须创建了知识库和域。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能设置域属性。  
  
##  <a name="set-domain-properties"></a><a name="Set"></a> 设置域属性  
  
1.  通过在域管理活动中打开某一知识库（请参阅 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)），然后在 **“域”** 列表中选择适当的域，对某一现有域设置属性。 默认情况下，将显示“域属性”页。  
  
2.  在按照 [Create a Domain](../data-quality-services/create-a-domain.md)中所述创建一个新域后设置其属性。  
  
3.  单击 **“完成”** 以完成域管理活动，如 [结束域管理活动](/previous-versions/sql/sql-server-2016/hh510411(v=sql.130))中所述。  
  
##  <a name="follow-up-after-setting-domain-properties"></a><a name="FollowUp"></a> 跟进：设置域属性后  
 在设置域属性后，您可以对域执行其他域管理任务，可以执行知识发现以便向域添加知识，或者可以向域添加匹配策略。 有关详细信息，请参阅[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)、[管理域](../data-quality-services/managing-a-domain.md)或[创建匹配策略](../data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="domain-properties"></a><a name="Properties"></a> 域属性  
  
###  <a name="domain-name-and-description"></a><a name="Name"></a> 域名和说明  
 一旦创建了一个域后，就可以更改该域名或说明。 对于知识库而言，域名必须唯一。 说明最多可以有 256 个字符。  
  
###  <a name="data-type"></a><a name="Type"></a> 数据类型  
 在您选择域后，为域中的值选择以下数据类型之一： **String** （默认设置）、 **Date**、 **Integer**或 **Decimal**。 在创建了域之后，可以查看数据类型，但不能更改数据类型。 为某个域选择的数据类型将定义可映射到该域的源数据的类型。 对于 DQS 中四个域数据类型支持的数据类型的相关信息，请参阅 [DQS 域支持的 SQL Server 和 SSIS 数据类型](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md)。  
  
###  <a name="use-leading-values"></a><a name="Leading"></a> 使用前导值  
 选中此复选框可指定将输出一组同义词中的前导值，而非是其同义词的值。 取消选择 **“使用前导值”** 可指定每个同义词值以其正确或更正形式输出，并且不会被其组的前导值替换。  
  
###  <a name="normalize-string"></a><a name="Normalize"></a> 规范化字符串  
 如果数据类型为 **String**，则请单击以忽略源数据中的特殊字符，以便 DQS 进行数据质量处理。 DQS 会在数据加载到域中时在内部用 null 或空格替换特殊字符。 冒号、连字符、句点、双引号或分号将替换为空格。 单引号将替换为 null。 使用 null 可使字符串的两个部分成为一体。  
  
 忽略字符串值中的特殊字符可提高匹配精确性。 可以通过使用 null 或空格替换特殊字符来增加两个字符串之间的相似性分数。 标点符号或其他符号可以轻松地在不同字符串之间进行区分。 通过在内部替换特殊字符，可使分数能够超过 DQS 中的最低匹配阈值，导致尚未匹配的两个字符串最终匹配。 但是，您是否选择忽略特殊字符可能依赖于您对其执行匹配的数据类型。 例如，当您在英制度量系统中使用数据时，如果双引号表示英寸，单引号表示英尺，则忽略产品数据中的双引号和单引号可能会导致误报。  
  
 当在发现、匹配策略、匹配项目和清理项目活动的数据处理阶段中加载和索引数据时，执行规范化。 如果启用，规范化和基于字词的关系转换都是在分析前的预处理阶段中进行的。 在应用计算字符串之间相似性的任何算法前对每个域执行它们。 如果请求复合域分析，将在规范化和基于字词的关系转换前执行分析，因为分隔符分析要求符号。 其他操作（例如域规则和域值更改）将会在转换后执行。 在 DQS 中内部替换特殊字符不会更改结果数据。  
  
###  <a name="format-output-to"></a><a name="Format"></a> 将输出格式设置为  
 选择在输出域中的数据值时要采用的格式。 此格式设置特定于选定的数据类型，如下面的列表中所示。 选择 **“无”** 意味着将不会在列表中应用任何格式。  
  
-   对于字符串值，您可以指定字符串将是输出为大写、小写还是首字母大写。  
  
-   对于日期值，您可以指定日、月和年的格式。  
  
-   对于整数值，您可以指定要应用的格式掩码的类型。  
  
-   对于小数值，您可以指定要应用的格式掩码的精确性和类型。  
  
###  <a name="language"></a><a name="Language"></a> 语言  
 如果数据类型为 **String**，则选择为用于拼写检查器操作而要将域与之关联的语言。 此选择仅适用于拼写检查器，因为拼写检查器结果取决于所用语言。 此选择仅适用于数据类型为字符串的单一域。 语言属性与复合域无关。 复合域中每个部分的语言由相关的单一域确定。  
  
 默认语言为英语。 将 **“语言”** 属性设置为 **“其他”** 将为该域禁用拼写检查器。  
  
> [!TIP]  
>  如果您的语言未列在 **“语言”** 下拉列表中，则必须选择 **“其他”**。 这可确保 DQS 根据域中可用的知识（域规则、域值、TBR、匹配规则），清理和消除未列出的语言数据的重复项。  
  
###  <a name="enable-speller"></a><a name="Speller"></a> 启用拼写检查器  
 如果数据类型是 **String**，则单击可为该域启用 DQS 拼写检查器。 拼写检查器仅适用于数据类型为字符串的域。 **“启用拼写检查器”** 复选框使拼写检查器仅适用于与该复选框相关联的单一域。 该复选框不适用于复合域。  
  
 拼写检查器会对域中的值建议语法和验证更正。 有关详细信息，请参阅 [Use the DQS Speller](../data-quality-services/use-the-dqs-speller.md)。  
  
###  <a name="disable-syntax-error-algorithms"></a><a name="Syntax"></a> 禁用语法错误算法  
 如果数据类型为 **String**，则选择此选项可指定在清理期间在域中 DQS 将不会标识语法错误。 在为该域标识语法错误无关紧要时选中此复选框。 例如，标识语法错误可能对于序列号无意义。 此控制仅可用于字符串数据类型。 DQS 不会检查非字符串数据类型是否有语法错误。  
  
