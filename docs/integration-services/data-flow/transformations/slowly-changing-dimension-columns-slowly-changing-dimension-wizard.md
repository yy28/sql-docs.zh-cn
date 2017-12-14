---
title: "渐变维度列（渐变维度向导）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cdf56b8da5d4c952c2202264125a9a48461f3e6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>渐变维度列（渐变维度向导）
  可以使用 **“渐变维度列”** 对话框，为每个渐变维度列选择更改类型。  
  
 若要了解有关此向导的详细信息，请参阅 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)。  
  
## <a name="options"></a>选项  
 **维度列**  
 从列表中选择维度列。  
  
 **更改类型**  
 选择“固定的属性”，或从两种变化的属性类型中选择一种类型。 在不需要更改列中的值时，请使用 **“固定的属性”** ；设置后， [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 会将更改视为错误。 若要使用更改后的值覆盖现有的值，请使用 **“变化的属性”** 。 若要在新记录中保存更改后的值，并将以前的记录标记为已过时，请使用 **“历史属性”** 。  
  
 **删除**  
 选择一个维度列，通过单击“删除”可以将其从映射列的列表中删除。  
  
## <a name="see-also"></a>另请参阅  
 [使用渐变维度向导配置输出](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
