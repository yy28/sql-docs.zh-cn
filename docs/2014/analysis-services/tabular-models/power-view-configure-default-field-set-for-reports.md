---
title: 为 Power View 报表配置默认字段集（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- ql12.asvs.bidtoolset.deffieldset.f1
ms.assetid: 6836b42f-28b8-4a98-a86d-2c3c109f0189
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 37571e141395afe255329edc10edeaeaed121710
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66066893"
---
# <a name="configure-default-field-set-for-power-view-reports-ssas-tabular"></a>配置 Power View 报表的默认字段集（SSAS 表格）
  默认字段集是一个列和度量值的预定义列表，当您选择报表字段列表中的表时，这些列和度量值会自动添加到 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 报表画布中。 表格模型作者可以创建默认字段集，使得将模型用于其报表的报表作者无需执行冗余步骤。 例如，如果您知道大多数使用客户联系信息的报表作者总是希望查看联系人姓名、主要电话号码、电子邮件地址和公司名称，您可以预先选择这些列，以便在作者单击客户联系表时，这些列总是会添加到报表画布中。  
  
> [!NOTE]  
>  默认字段集仅应用于 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]中用作数据模型的表格模型。 Excel 透视报表不支持默认字段集。  
  
## <a name="creating-a-default-field-set"></a>创建默认字段集  
 您可以确定当在 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]中选择某个特定表时，默认情况下包含的字段（如果有）。 还可以确定这些字段在列表中的显示顺序。 若要指定默认字段集，您可以在表格模型项目中设置报表属性。  
  
#### <a name="to-add-a-default-field-set"></a>添加默认字段集  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击要为其配置默认字段列表的表。  
  
2.  在 **“属性”** 窗口的 **“默认字段集”** 属性中，单击 **“单击可编辑”**。  
  
3.  在“默认字段集”对话框中，选择一个或多个字段。 可以选择表中的任何字段，包括度量值。 按住 Shift 键以选择范围，或按住 Ctrl 键以选择单个字段。  
  
4.  单击 **“添加”** 以将其添加到默认字段集。  
  
5.  使用“上移”和“下移”按钮指定字段列表的顺序。 按照为字段集定义的顺序将字段添加到报表中。  
  
6.  对工作簿中的其他表重复这些步骤。  
  
## <a name="next-step"></a>下一步  
 创建默认字段集后，您可以通过指定默认标签、默认图像、默认组行为或是将包含相同值的各个行组合到一个行中还是分别列出这些行，来进一步影响报表设计体验。 有关详细信息，请参阅[为 Power View 报表配置表行为属性（SSAS 表格）](power-view-configure-table-behavior-properties-for-reports.md)。  
  
  
