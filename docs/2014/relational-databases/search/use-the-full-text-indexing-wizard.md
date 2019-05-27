---
title: 使用全文索引向导 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextindexingwizard.selecttablecolumns.f1
- sql12.swb.fulltextindexingwizard.welcome.f1
- sql12.swb.fulltextindexingwizard.selectacatalog.f1
- sql12.swb.fulltextindexingwizard.progress.f1
- sql12.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql12.swb.fulltextindexingwizard.selectatableorview.f1
- sql12.swb.fulltextindexingwizard.selectchangetracking.f1
- sql12.swb.fulltextindexingwizard.selectanindex.f1
- sql12.swb.fulltextindexingwizard.summary.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f7bab4ee8f03eb666e1a8396fbf8957b1e42f2c7
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010901"
---
# <a name="use-the-full-text-indexing-wizard"></a>使用全文索引向导
  全文索引向导可引导您完成一系列步骤，以帮助您创建全文索引。  
  
#### <a name="to-use-the-full-text-indexing-wizard"></a>使用全文索引向导  
  
1.  在对象资源管理器中，右键单击要对其创建全文索引的表，指向“全文索引”，然后单击“定义全文索引”。  
  
     **唯一索引**  
     从下拉列表中选择索引。 索引必须是唯一且不为 Null 的单键列索引。 为全文唯一键选择最小的唯一键索引。 为了获得最佳性能，建议使用聚集索引。  
  
     **可用列**  
     若要在索引中包括某列，请选中该列名旁边的复选框。 不能够进行全文索引的列显示为灰色，并禁用其复选框。  
  
     **断字符语言**  
     从下拉列表中选择语言。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将使用此选项为索引标识正确的断字符。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用断字符在全文索引的数据中标识词的边界。  
  
     **类型列**  
     选择存储作为全文索引列的文档类型的列名称。  
  
     **类型列**仅当列中命名的启用**可用列**列的类型是`varbinary(max)`或`image`。  
  
     **统计语义**  
     选择是否为所选列启用语义索引。 有关详细信息，请参阅[语义搜索 (SQL Server)](semantic-search-sql-server.md)。  
  
     如果您在选择 **“统计语义”** 前选择某一 **“语言”**，并且所选语言没有关联的语义语言模型，则 **“统计语义”** 复选框将被禁用。 如果你在选择“语言”前选择“统计语义”，则下拉组合框中提供的语言将限制为存在语义语言模型支持的那些语言。  
  
2.  选择更改跟踪选项。  
  
     **自动**  
     选中此单选按钮后，当基础数据发生更改时，全文索引将自动更新。  
  
     **手动**  
     如果不希望基础数据发生更改时自动更新全文索引，请选中此单选按钮。 对基础数据的更改将保留下来。 不过，若要将更改应用到全文索引，必须手动启动或安排此进程。  
  
     **不跟踪更改**  
     如果不希望使用基础数据的更改对全文索引进行更新，请选中此单选按钮。  
  
     **创建索引时启动完全填充**  
     选中此单选按钮，可以在此向导成功完成后启动完全填充。 这将包括在目录中创建全文索引结构，并用全文索引的数据对其进行填充。  
  
3.  选择目录、索引文件组和非索引字表。  
  
     **选择全文目录**  
     从列表中选择全文目录。 默认情况下，数据库的默认目录为该列表中选定的项。 如果没有可用的目录，则该列表将处于禁用状态，并且 **“创建新目录”** 复选框将处于选中状态并被禁用。  
  
    |||  
    |-|-|  
    |**“创建新目录”**|选中此复选框可以创建新的全文目录。|  
  
     **名称**  
     为新的全文目录输入一个名称。  
  
     **设置为默认目录**  
     选中此项可以将该目录设为此数据库的默认目录。  
  
     **区分重音**  
     指定新目录是区分重音还是不区分重音。 如果数据库区分重音，默认情况下会选中“区分”。  
  
     **选择索引文件组**  
     指定对其创建全文索引的文件组。  
  
     选择下列值之一：  
  
    |ReplTest1|Description|  
    |-----------|-----------------|  
    |**\<default>**|如果表或视图尚未分区，则选择此值，将与基础表或视图使用相同的文件组。 如果表或视图已分区，则使用主文件组。|  
    |**PRIMARY**|选择此值可将主文件组用于新全文索引。|  
    |*用户指定的默认文件组*|如果存在用户定义的默认非索引字表，请从列表选择其名称，可将该文件组用于新全文索引。|  
  
     **选择全文非索引字表**  
     指定要用于全文索引的非索引字表，或者禁用非索引字表。  
  
     在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更高版本中，使用称为“非索引字表”的对象在数据库中管理非索引字。 “非索引字表”是一个由非索引字组成的列表，这些非索引字在与全文检索关联时会应用于该索引的全文查询。 有关详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
     选择下列值之一：  
  
    |ReplTest1|Description|  
    |-----------|-----------------|  
    |**\<system>**|选择此值将对新全文索引使用系统非索引字表。 这是默认值。|  
    |**\<off>**|选择此值将禁用新全文索引的非索引字表。|  
    |*用户定义的非索引字表名称*|该列表显示已对数据库创建的用户定义的每个非索引字表（如果有）的名称。 选择任何要用于新全文索引的用户定义的非索引字表。|  
  
4.  定义填充计划（可选）。 索引操作将立即开始，除非已将其安排为在将来执行。 此时将立即创建计划，尽管在计划时间之前并不会运行这些计划。  
  
     **新建表计划**  
     定义表的填充计划。  
  
     **新建目录计划**  
     定义全文目录的填充计划。  
  
     **编辑**  
     编辑计划。  
  
     **删除**  
     删除计划。  
  
5.  查看或控制全文索引向导的进度。  
  
     **停止**  
     中断当前操作，并阻止该向导在此会话期间执行后续全文操作。  
  
     **报告**  
     当执行完所有操作以后，单击此按钮可以访问所执行操作的报告。 您可以查看该报告，将其打印为文件，复制到剪贴板，或用电子邮件发送该报告。  
  
  
