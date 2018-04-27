---
title: 匹配相似数据 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: microsoft-excel-add-in
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f6fd6fc1-3569-42a5-b6cb-87a921c88f3b
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b83a1248f81d52b97f3205d1e74eb408c820698
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="match-similar-data-mds-add-in-for-excel"></a>匹配相似数据（用于 Excel 的 MDS 外接程序）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，使用 Data Quality Services (DQS) 功能查找数据中的相似性。  
  
 若要执行此过程，您可以：  
  
-   使用默认的 Data Quality Services 知识库，或  
  
-   创建您自己的自定义 DQS 知识库和匹配策略。 有关详细信息，请参阅 [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md)。  
  
## <a name="prerequisites"></a>必备条件  
  
-   必须具有包含 MDS 管理的数据的工作表。 有关详细信息，请参阅 [从 Master Data Services 中将数据导出至 Excel](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)。  
  
-   可选。 您可以在检查是否存在相似性之前将其他数据和 MDS 管理的数据合并在一起。 有关详细信息，请参阅 [合并数据（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)。  
  
### <a name="to-find-similarities-by-using-the-default-knowledge-base"></a>使用默认知识库查找相似性  
  
1.  从包含 MDS 管理的数据的工作表中，在“数据质量”组中单击“匹配数据”。  
  
2.  在“匹配数据”对话框中，从“DQS 知识库”列表中选择“DQS 数据(默认)”。  
  
3.  对于包含要匹配的数据的每个列，在该对话框中添加一行。 有关此对话框中字段的详细信息，请参阅 [How to Set Matching Rule Parameters](../../data-quality-services/create-a-matching-policy.md#MatchingRules)。  
  
4.  在所有权重值的总和等于 100% 时，单击 **“确定”**。  
  
### <a name="to-find-similarities-by-using-a-custom-knowledge-base"></a>使用自定义知识库查找相似性  
  
1.  从包含 MDS 管理的数据的工作表中，在“数据质量”组中单击“匹配数据”。  
  
2.  从 **“DQS 知识库”** 列表中，选择您的自定义知识库的名称。  
  
3.  对于该工作表中每一列，选择一个 DQS 域。  
  
4.  在所有 DQS 域都映射到该工作表中的列后，单击 **“确定”**。  
  
## <a name="next-steps"></a>Next Steps  
  
-   查看其他信息以便确定哪些数据是类似的。 有关详细信息，请参阅[数据质量匹配列（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/data-quality-matching-columns-mds-add-in-for-excel.md)。  
  
## <a name="see-also"></a>另请参阅  
 [用于 Excel 的 MDS 外接程序中的数据质量匹配](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [数据匹配](../../data-quality-services/data-matching.md)  
  
  
