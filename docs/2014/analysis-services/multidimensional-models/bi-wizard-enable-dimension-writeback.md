---
title: 启用维度写回 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying dimensions
- writeback [Analysis Services], setting up
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], writeback
- dimensions [Analysis Services], writeback
- writeback [Analysis Services]
- dimensions [Analysis Services], modifying
- manual dimension structure modifications
ms.assetid: a4b5eb5a-366d-4fc8-ad0d-5bdb8e7b4163
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6051f62caac2878b689a50e5773b047cb8df7afe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076853"
---
# <a name="enable-dimension-writeback"></a>“启用维度写回”
  通过为多维数据集或维度添加维度写回增强功能，可以使用户手动修改维度结构和成员。 对允许写维度的更新直接记录在该维度表中。 此增强功能更改了维度的 `WriteEnabled` 属性设置。  
  
 若要添加维度写回，请使用商业智能向导，然后在 **“选择增强功能”** 页中选择 **“启用维度写回”** 选项。 然后，此向导将指引您完成相应的步骤，以选择要应用维度写回的维度，并为所选维度设置此选项。  
  
> [!NOTE]  
>  仅对 SQL Server 关系数据库和数据市场支持写回。  
  
## <a name="selecting-a-dimension"></a>选择维度  
 在向导的第一个 **“启用维度写回”** 页中，指定要应用维度写回的维度。 为该所选维度添加的维度写回增强功能将导致维度发生更改。 所有包含选定维度的多维数据集都将继承这些更改。  
  
## <a name="setting-dimension-writeback-capability"></a>设置维度写回功能  
 在向导的第二个 **“启用维度写回”** 页中，实际设置 **“在维度中启用写回”** 选项。 选择此选项将使维度的 `WriteEnabled` 属性自动设置为 `True`。 清除此选项将使该属性自动设置为 `False`。  
  
## <a name="remarks"></a>备注  
 创建新成员时，必须包括维度中的所有属性。 您不能插入未指定维度的键属性值的成员。 因此，创建成员时，应服从对维度表定义的任何约束（例如，非空键值）。 您还应该考虑可能由维度属性指定的列，例如在 `CustomRollupColumn`、`CustomRollupPropertiesColumn` 或 `UnaryOperatorColumn` 维度属性中指定的列。  
  
> [!WARNING]  
>  如果您使用 SQL Azure 作为数据源来执行写回到 Analysis Services 数据库，则该操作将失败。 这是默认设置，因为默认不启用实现多个活动的结果集 (MARS) 的提供程序选项。  
>   
>  解决方法是在连接字符串中添加以下设置，以便支持 MARS 并启用写回：  
>   
>  `"MultipleActiveResultSets=True"`  
>   
>  有关详细信息，请参阅[使用多个活动的结果集 (MARS)](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)。  
  
## <a name="see-also"></a>请参阅  
 [启用写操作的维度](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
