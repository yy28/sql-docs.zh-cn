---
title: 数据质量项目 (DQS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a43fc9c0-19b6-414a-8661-4c7c55e0c03e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: fe1d4272f89c962784a8716da143180ae2b12aa1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480863"
---
# <a name="data-quality-projects-dqs"></a>数据质量项目 (DQS)
  
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的数据质量项目就是使用知识库，通过执行“数据清理” ** 和 ** “数据匹配”活动改进源数据的质量，然后将结果数据导出到 SQL Server 数据库或 .csv 文件。 您可以将数据质量项目创建为一个清理项目或匹配项目，以执行相应的任务。 可以通过使用同一个知识库运行清理项目和匹配项目，因为用于数据清理和匹配的知识可以内置于同一个知识库中。  
  
 数据质量项目具有以下优点：  
  
-   使您可以通过使用 DQS 知识库中的知识对您的数据源执行数据清理。  
  
-   使您可以通过使用知识库中的匹配策略对您的数据源执行数据匹配。  
  
-   提供一个向导，指导您完成整个清理活动和匹配活动，并根据您的选择将数据导出到 SQL Server 数据库或 .csv 文件。 数据专员可以使用数据质量项目来运行并控制计算机辅助/交互方式清理步骤和数据匹配步骤。  
  
##  <a name="Cleansing"></a>数据质量项目：清理活动  
 清理数据质量项目使您可以基于知识库清理您的源数据。 DQS 中的数据清理活动分为两个步骤：  
  
1.  “计算机辅助” ** 数据清理过程，可以针对知识库中的知识分析源数据并提出更改建议。 DQS 对处理后的数据进行分类（建议、新建、无效、已更正和正确），然后向用户显示以供进一步处理。  
  
2.  “交互式” ** 清理过程，使数据专员可以批准、拒绝或修改计算机辅助数据清理过程建议的数据。  
  
 有关数据质量项目中的清理活动的详细信息，请参阅 [Data Cleansing](../../2014/data-quality-services/data-cleansing.md)。  
  
##  <a name="Matching"></a>数据质量项目：匹配活动  
 匹配数据质量项目支持您基于知识库中的匹配策略执行匹配活动，通过标识精确匹配项和近似匹配项，进而删除重复数据，以防止数据重复。 建议先清除数据，然后再运行匹配。 为此，请执行以下操作：  
  
1.  创建数据质量项目，选择 **“清理”** 活动，对源数据完成数据清理活动，然后将其导出到 SQL Server 数据库中的表。  
  
2.  通过使用包含匹配策略的知识库创建另一个数据质量项目，选择 **“匹配”** 活动，然后在 **“映射”** 页中，选择在步骤 1 中导出已清理数据的数据库和表。  
  
3.  完成针对已清理数据的匹配活动。  
  
 有关数据质量项目中的匹配活动的详细信息，请参阅 [Data Matching](../../2014/data-quality-services/data-matching.md)。  
  
##  <a name="ProfilingNotification"></a>数据事件探查和通知  
 在数据质量项目中运行清理和匹配活动时，可查看与正由 DQS 处理的数据有关的实时统计信息和其他信息。 数据事件探查可帮助您评估清理或匹配过程的有效性，并且您可能能够确定数据清理或数据匹配在多大程度上可帮助您提高数据质量。 DQS 事件探查提供两种数据质量维度：“完整性” ** （提供数据的范围）和“准确性” ** （数据可用于目标用途的程度）。 此外，根据数据事件探查信息，对用户显示相关的通知，告知用户可以通过采取哪些措施来改善数据清理和数据匹配操作。 有关数据事件探查和通知的详细信息，请参阅 [Data Profiling and Notifications in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|描述如何创建数据质量项目。|[创建数据质量项目](../../2014/data-quality-services/create-a-data-quality-project.md)|  
|描述如何管理（打开、解锁、重命名和删除）数据质量项目。|[管理数据质量项目&#41; &#40;打开、解锁、重命名和删除](../../2014/data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md)|  
|描述如何在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中打开 Integration Services 项目。|[在 Data Quality Client 中打开 Integration Services 项目](../../2014/data-quality-services/open-integration-services-projects-in-data-quality-client.md)|  
  
## <a name="see-also"></a>另请参阅  
 [DQS 知识库和域](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
