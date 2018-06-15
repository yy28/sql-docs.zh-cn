---
title: 添加详细信息组（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5ef8efba-6d48-4aeb-a3b9-a02ba5a44614
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b8c504724523a3e331a54137766504b3599587c2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33019754"
---
# <a name="add-a-details-group-report-builder-and-ssrs"></a>添加详细信息组（报表生成器和 SSRS）
在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表中，报表数据集的详细信息数据指定为不包含组表达式的组。 要显示矩阵的详细信息数据、重新添加已从表或列表中删除的详细信息数据或添加其他详细信息组时，请向现有 tablix 数据区域添加详细信息组。 有关组的详细信息，请参阅 [了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-details-group-to-a-tablix-data-region"></a>向 tablix 数据区域添加详细信息组  
  
1.  在设计图面上，单击选定 tablix 数据区域中的任意位置。 “分组”窗格将显示选定数据区域的行组和列组。  
  
2.  在“分组”窗格中，右键单击作为最内部的子组的组。 单击 **“添加组”**，然后单击 **“子组”**。 此时将打开 **“Tablix 组”** 对话框。  
  
3.  在 **“组表达式”** 中，使表达式保留为空白。 详细信息组没有任何表达式。  
  
4.  选择 **“显示详细信息数据”**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     新的详细信息组作为子组添加到“分组”窗格，在步骤 1 中选择的组的行控点显示详细信息组图标。 有关控点的详细信息，请参阅 [Tablix 数据区域单元、行和列（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [了解组（报表生成器和 SSRS）](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-report-builder-and-ssrs.md) [矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
