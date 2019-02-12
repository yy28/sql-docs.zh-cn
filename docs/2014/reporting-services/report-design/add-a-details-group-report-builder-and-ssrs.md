---
title: 添加详细信息组（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5ef8efba-6d48-4aeb-a3b9-a02ba5a44614
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9e6b467700d816e4b46dfa7ae38f67be32234c7d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041788"
---
# <a name="add-a-details-group-report-builder-and-ssrs"></a>添加详细信息组（报表生成器和 SSRS）
  报表数据集的详细信息数据指定为不包含组表达式的组。 要显示矩阵的详细信息数据、重新添加已从表或列表中删除的详细信息数据或添加其他详细信息组时，请向现有 tablix 数据区域添加详细信息组。 有关组的详细信息，请参阅 [了解组（报表生成器和 SSRS）](understanding-groups-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-details-group-to-a-tablix-data-region"></a>向 tablix 数据区域添加详细信息组  
  
1.  在设计图面上，单击选定 tablix 数据区域中的任意位置。 “分组”窗格将显示选定数据区域的行组和列组。  
  
2.  在“分组”窗格中，右键单击作为最内部的子组的组。 单击 **“添加组”**，然后单击 **“子组”**。 此时将打开 **“Tablix 组”** 对话框。  
  
3.  在 **“组表达式”** 中，使表达式保留为空白。 详细信息组没有任何表达式。  
  
4.  选择 **“显示详细信息数据”**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     新的详细信息组作为子组添加到“分组”窗格，在步骤 1 中选择的组的行控点显示详细信息组图标。 有关控点的详细信息，请参阅 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [在数据区域中添加或删除组（报表生成器和 SSRS）](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [了解组（报表生成器和 SSRS）](understanding-groups-report-builder-and-ssrs.md)   
 [Tablix 数据区域（报表生成器和 SSRS）](../tablix-data-region-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
