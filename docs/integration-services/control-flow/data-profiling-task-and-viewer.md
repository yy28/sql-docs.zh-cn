---
title: 数据事件探查任务和查看器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], about data profiling
- data profiling
- profiling data
ms.assetid: 756840e3-aa09-45cd-9951-1a17af4b5925
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6301066549a8008512bef934f9d887349a6b765b
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727775"
---
# <a name="data-profiling-task-and-viewer"></a>数据事件探查任务和查看器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  数据事件探查任务在提取、转换和加载数据的过程中提供数据事件探查功能。 使用数据事件探查任务，有以下好处：  
  
-   更有效地分析源数据  
  
-   更好地了解源数据  
  
-   将数据引入数据仓库之前防止数据质量问题。  
  
> [!IMPORTANT]  
>  数据事件探查任务仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储的数据。 它不适用于第三方或基于文件的数据源。  
  
## <a name="data-profiling-overview"></a>数据事件探查概述  
 数据质量对所有业务都至关重要。 由于企业将分析和业务智能系统建立在他们的事务系统之上，因此关键绩效指标和数据挖掘预测的可靠性完全取决于所依据的数据的有效性。 不过，尽管数据的有效性对于业务决策越来越重要，但如何确保该数据有效也越来越具有挑战性。 因为，数据在源源不断地从各种系统和源以及大量用户处流入企业。  
  
 数据质量的度量难以定义，原因是度量特定于域或应用程序。 一个常用的定义数据质量的方法就是数据事件探查。  
  
 数据配置文件是聚合统计信息的集合，其中可能包含下面的信息：  
  
-   Customer 表中的行数。  
  
-   State 列中非重复的值的数目。  
  
-   Zip 列中 null 值或缺失值的数目。  
  
-   City 列中值的分布。  
  
-   State 列对 Zip 列的函数依赖强度，即对于指定的邮政编码值，省/市/自治区应始终是一样的。  
  
 数据配置文件提供的统计信息为您提供了所需信息，可以有效地最大限度降低使用源数据过程中可能出现的质量问题。  
  
## <a name="integration-services-and-data-profiling"></a>Integration Services 和数据事件探查  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，数据事件探查过程包括以下步骤：  
  
 **步骤 1：设置数据事件探查任务**  
 数据事件探查任务是用于配置要计算的配置文件的任务。 运行包含数据事件探查任务的包以计算配置文件。 该任务将配置文件输出以 XML 格式保存到文件或包变量。  
  
 **详细信息：**[设置数据事件探查任务](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)  
  
 **步骤 2：查看数据事件探查任务计算的配置文件**  
 若要查看数据事件探查任务计算的数据配置文件，请将输出发送到文件，然后使用数据配置文件查看器。 此查看器是一种独立的实用工具，可以通过可选的明细功能以摘要的格式和以详细信息的格式显示配置文件输出。  
  
 **详细信息：**[数据配置文件查看器](../../integration-services/control-flow/data-profile-viewer.md)  
  
### <a name="addition-of-conditional-logic-to-the-data-profiling-workflow"></a>向数据事件探查工作流添加条件逻辑  
 数据事件探查任务不包含内置功能，即无法根据配置文件输出使用条件逻辑来将此任务连接到下游任务。 但是，您只要在脚本任务中进行少量的编程工作即可轻松地添加此逻辑。 例如，脚本任务可以对数据事件探查任务的输出文件执行 Xpath 查询。 该查询可以确定在特定列中 null 值的百分比是否超过特定的阈值。 如果该百分比超过阈值，则应中断包并解决源数据中的问题，然后再继续执行。 有关详细信息，请参阅 [合并包工作流中的数据分析任务](../../integration-services/control-flow/incorporate-a-data-profiling-task-in-package-workflow.md)。  
  
## <a name="related-content"></a>相关内容  
 [数据探查器架构](https://go.microsoft.com/fwlink/?LinkId=251524)  
  
  
