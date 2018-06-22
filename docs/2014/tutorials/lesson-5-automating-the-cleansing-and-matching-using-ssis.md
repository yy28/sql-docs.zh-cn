---
title: 第 5 课： 自动清理和匹配使用 SSIS |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 00dff9ac204e5e1b86feafc51da643222bce1758
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015816"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>第 5 课：使用 SSIS 自动执行清理和匹配
  在第 1 课中，可以生成供应商知识库和用它来清理在第 2 课中的数据和匹配中使用工具第 3 课数据**DQS 客户端**。 在实际方案中，你可能需要从 DQS 不支持或你想要自动清理的源和匹配过程中请求数据，而无需使用**DQS 客户端**工具。 SQL Server Integration Services (SSIS) 具有可用于将来自各种异类源的数据集成的组件和**[超链接"http://msdn.microsoft.com/library/ee677619.aspx"\t"_blank"DQS 清理转换](http://msdn.microsoft.com/library/ee677619.aspx)** 要为其调用公开的 DQS 清理功能的组件。 目前，DQS 不公开匹配功能 for SSIS 若要使用，但你可以使用**[模糊分组转换](http://msdn.microsoft.com/library/ms141764.aspx)** 来标识数据中的重复。  
  
 你可以将数据上载到 MDS 使用**基于实体的临时功能**。 在 MDS 中创建实体时，将自动创建相应的临时表和存储过程。 例如，当你创建的供应商实体， **stg.supplier_Leaf**表和**stg.udp_Supplier_Leaf**自动创建存储的过程。 您可以使用临时表和过程来创建、更新和删除实体成员。 在本课中，您将为 Supplier 实体创建新实体成员。 要将数据加载到 MDS 服务器中，SSIS 包首先将数据加载到临时表 stg.supplier_Leaf 中，然后触发关联的存储过程 stg.udp_Supplier_Leaf。 请参阅[导入数据](http://msdn.microsoft.com/library/ee633726.aspx)有关详细信息。  
  
 在本课中，您将执行以下任务：  
  
1.  在 MDS 中删除供应商数据（如果您学完了前四课）。 您在本课中创建的 SSIS 包自动将数据上载到 MDS。 之前，您使用 DQS 客户端手动将清理和匹配的供应商数据上载到了 MDS 服务器。  
  
2.  在 Supplier 实体上创建订阅视图，以便向其他应用程序公开此实体中的数据。 此操作会创建一个您将使用 SQL Server Management Studio 验证的 SQL 视图。 在这一版本的教程中，您不使用此视图。  
  
3.  创建并使用运行的 SSIS 项目**SQL Server Data Tools**。 项目使用**数据清理**转换提交清理请求到 DQS 服务器。 DQS 不公开的匹配功能，因此你将使用**模糊分组**转换来标识重复。  
  
4.  验证通过使用“主数据管理器”在 MDS 中创建了数据。  
  
5.  查看由 SSIS 包创建的 DQS 清理项目的结果，并可选执行交互式清理以进一步生成知识库。  
  
## <a name="next-step"></a>下一步  
 [任务 1&#40;先决条件&#41;： 在 MDS 中删除供应商的数据](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  