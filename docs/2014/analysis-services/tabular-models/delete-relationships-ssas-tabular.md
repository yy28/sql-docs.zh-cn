---
title: 删除关系 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d40e3f05-54e8-4c4b-807a-0b06f446079b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3be65edb0300b2ab47f22784cb7b109372062e0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62795454"
---
# <a name="delete-relationships-ssas-tabular"></a>删除关系（SSAS 表格）
  您可以使用模型设计器中的“关系图视图”或使用“管理关系”对话框来删除现有关系。 有关如何在表格模型中使用关系的详细信息，请参阅 [关系（SSAS 表格）](relationships-ssas-tabular.md)。  
  
## <a name="considerations-for-deleting-relationships"></a>删除关系时的注意事项  
 决定是否删除关系时要注意下列问题：  
  
-   无法撤消删除关系。 您可以重新创建关系，但此操作要求完全重新计算模型中的公式。 因此，在删除在公式中使用的关系前，应始终首先进行检查。  
  
-   删除两个表之间的关系会导致引用这些表的公式中出现错误。  
  
-   数据分析表达式 (DAX) RELATED 函数使用表之间的关系查找其他表中的相关值。 关系删除之后，该函数将返回不同的结果。 有关详细信息，请参阅 RELATED 函数 (DAX)。  
  
-   除了更改数据透视表和公式的结果以外，创建和删除关系还将导致重新计算工作簿，这可能需要一些时间。  
  
## <a name="delete-relationships"></a>删除关系  
  
#### <a name="to-delete-a-relationship-by-using-diagram-view"></a>使用“关系图视图”删除关系  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后指向 **“模型视图”**，再单击 **“关系图视图”**。  
  
2.  右键单击两个表之间的关系线，然后单击“删除”。  
  
#### <a name="to-delete-a-relationship-by-using-the-manage-relationships-dialog-box"></a>使用“管理关系”对话框删除关系  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，单击 **“表”** 菜单，然后单击 **“管理关系”**。  
  
2.  在 **“管理关系”** 对话框中，从列表中选择一个或多个关系。  
  
     若要选择多个关系，请按住 Ctrl 键，同时单击各个关系。  
  
3.  单击 **“删除关系”**。  
  
4.  在 **“管理关系”** 对话框中，单击 **“关闭”**。  
  
## <a name="see-also"></a>请参阅  
 [关系（SSAS 表格）](relationships-ssas-tabular.md)   
 [创建两个表之间的关系（SSAS 表格）](create-a-relationship-between-two-tables-ssas-tabular.md)  
  
  
