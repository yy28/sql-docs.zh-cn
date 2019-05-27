---
title: 手动处理数据 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.datarefreshprogressdb.f1
ms.assetid: 0918c04c-c1e6-45b4-acfa-96fa578e684b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5de1215bd9646e115c6b2730c4e8a750a3f4040f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077965"
---
# <a name="manually-process-data-ssas-tabular"></a>手动处理数据（SSAS 表格）
  本主题说明如何手动处理 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中的工作区数据。  
  
 如果您创作表格模型时使用了外部数据，则可以使用“处理”命令手动刷新这些数据。 您可以处理单个表、模型中的所有表或一个或多个分区。 只要处理数据，就还可能需要重新计算数据。  处理数据意味着从外部源中获取最新的数据。 “重新计算”意味着更新使用数据的任何公式的结果。  
  
 本主题的内容：  
  
-   [手动处理数据](#bkmk_mahually_process)  
  
-   [数据处理进度](#bkmk_data_process_progress)  
  
##  <a name="bkmk_mahually_process"></a> 手动处理数据  
  
#### <a name="to-process-data-for-a-single-table-or-all-tables-in-a-model"></a>处理模型中单个表或者所有表的数据  
  
1.  在模型设计器中，单击要处理的表。  
  
2.  单击 **“模型”** 菜单，然后单击 **“处理”**，再单击 **“处理”** 或 **“全部处理”**。  
  
#### <a name="to-process-data-for-all-tables-using-the-same-connection"></a>处理使用相同连接的所有表的数据  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“现有连接”**。  
  
2.  在 **“现有连接”** 对话框中，选择某一连接，然后单击 **“处理”**。  
  
#### <a name="to-process-data-for-one-or-more-partitions"></a>处理一个或多个分区的数据  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后指向 **“处理”**，再单击 **“处理分区”**。  
  
2.  在 **“处理分区”** 对话框的 **“模式”** 中，选择下列处理模式之一：  
  
    |“模式”|Description|  
    |----------|-----------------|  
    |**处理默认值**|检测分区对象的处理状态，执行必要的处理，将未处理的分区对象或部分处理的分区对象交付为已完全处理的分区对象。 为空表和分区加载数据；生成或重新生成层次结构、计算列和关系。|  
    |**处理全部**|处理分区对象及其包含的所有对象。 对已处理的对象运行“处理全部”时， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将删除该对象中的所有数据，然后再处理该对象。 在对对象进行结构更改后，需要这种类型的处理。|  
    |**处理数据**|将数据加载到分区或表中，而无需重新生成层次结构或关系或重新计算计算列和度量值。|  
    |**处理清除**|删除分区中的所有数据。|  
    |**处理添加**|以增量方式用新数据更新分区。|  
  
3.  在分区列表中，选择要处理的分区，然后单击 **“确定”**。  
  
##  <a name="bkmk_data_process_progress"></a> 数据处理进度  
 **“数据处理进度”** 对话框可用于监视从外部数据源导入到模型中的数据的处理。 若要访问此对话框，请依次单击 **“模型”** 菜单、 **“处理分区”**、 **“处理表”** 或 **“全部处理”**。  
  
 **“状态”**  
 指示处理操作是否成功。  
  
 **详细信息**  
 列出导入的表和视图，导入的行数，并提供一个指向任何问题报告的链接。  
  
 **停止刷新**  
 单击此选项可以暂停处理操作。 如果操作用时过长或出现太多错误，则此选项很有用。  
  
## <a name="see-also"></a>请参阅  
 [处理数据（SSAS 表格）](process-data-ssas-tabular.md)   
 [数据处理故障排除（SSAS 表格）](troubleshoot-process-data-ssas-tabular.md)  
  
  
