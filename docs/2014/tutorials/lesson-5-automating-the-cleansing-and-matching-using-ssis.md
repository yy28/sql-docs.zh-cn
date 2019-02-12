---
title: 第 5 课：自动执行清理和匹配使用 SSIS |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 92261bc69590bcc338bf18aa9d406964bfe42fcd
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026628"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>第 5 课：使用 SSIS 自动执行清理和匹配
  第 1 课中生成 Suppliers 知识库和用它来清理第 2 课中的数据和匹配数据中使用该工具第 3 课**DQS 客户端**。 在实际方案中，您可能需要从 DQS 不支持或你想要自动执行清理的源和匹配过程中提取数据，而无需使用**DQS 客户端**工具。 SQL Server Integration Services (SSIS) 具有可用于将来自各种异构源的数据集成的组件和一个 **[DQS 清理转换](https://msdn.microsoft.com/library/ee677619.aspx)** 组件，可调用清理dqs 公开的功能。 目前，DQS 不会公开匹配功能供 SSIS 使用，但你可以使用**[模糊分组转换](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)** 来确定数据中的重复项。  
  
 您可以使用将数据上载到 MDS**基于实体的临时处理功能**。 在 MDS 中创建实体时，将自动创建相应的临时表和存储过程。 例如，您创建 Supplier 实体时， **stg.supplier_Leaf**表和**stg.udp_Supplier_Leaf**自动创建存储的过程。 您可以使用临时表和过程来创建、更新和删除实体成员。 在本课中，您将为 Supplier 实体创建新实体成员。 要将数据加载到 MDS 服务器中，SSIS 包首先将数据加载到临时表 stg.supplier_Leaf 中，然后触发关联的存储过程 stg.udp_Supplier_Leaf。 请参阅[导入数据](../master-data-services/overview-importing-data-from-tables-master-data-services.md)的更多详细信息。  
  
 在本课中，您将执行以下任务：  
  
1.  在 MDS 中删除供应商数据（如果您学完了前四课）。 您在本课中创建的 SSIS 包自动将数据上载到 MDS。 之前，您使用 DQS 客户端手动将清理和匹配的供应商数据上载到了 MDS 服务器。  
  
2.  在 Supplier 实体上创建订阅视图，以便向其他应用程序公开此实体中的数据。 此操作会创建一个您将使用 SQL Server Management Studio 验证的 SQL 视图。 在这一版本的教程中，您不使用此视图。  
  
3.  创建并使用运行 SSIS 项目**SQL Server Data Tools**。 该项目使用**数据清理**转换以提交清理请求到 DQS 服务器。 DQS 不公开匹配功能，因此您将使用**模糊分组**转换以确定重复项。  
  
4.  验证通过使用“主数据管理器”在 MDS 中创建了数据。  
  
5.  查看由 SSIS 包创建的 DQS 清理项目的结果，并可选执行交互式清理以进一步生成知识库。  
  
## <a name="next-step"></a>下一步  
 [任务 1&#40;先决条件&#41;:删除 MDS 中的供应商数据](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
