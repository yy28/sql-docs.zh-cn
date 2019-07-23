---
title: 渐变维度列（渐变维度向导）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: dcf11c5ebb6372ecea9e056577524de50a169747
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943990"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>渐变维度列（渐变维度向导）

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  可以使用 **“渐变维度列”** 对话框，为每个渐变维度列选择更改类型。  
  
 若要了解有关此向导的详细信息，请参阅 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)。  
  
## <a name="options"></a>选项  
 **维度列**  
 从列表中选择维度列。  
  
 **更改类型**  
 选择“固定的属性”，或从两种变化的属性类型中选择一种类型。  在不需要更改列中的值时，请使用 **“固定的属性”** ；设置后， [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 会将更改视为错误。 若要使用更改后的值覆盖现有的值，请使用 **“变化的属性”** 。 若要在新记录中保存更改后的值，并将以前的记录标记为已过时，请使用 **“历史属性”** 。  
  
 **删除**  
 选择一个维度列，通过单击“删除”可以将其从映射列的列表中删除。   
  
## <a name="see-also"></a>另请参阅  
 [使用渐变维度向导配置输出](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
