---
title: 维度类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- time dimensions [Analysis Services]
- quantitative dimensions [Analysis Services]
- BillOfMaterials dimension [Analysis Services]
- geography dimensions
- utility dimensions [Analysis Services]
- channel dimensions
- dimensions [Analysis Services], types
- products dimensions [Analysis Services]
- account dimensions [Analysis Services]
- organization dimensions
- currency dimensions [Analysis Services]
- rates dimensions
- promotion dimensions
- scenario dimensions [Analysis Services]
- customers dimensions [Analysis Services]
- Type property
ms.assetid: bd3195da-e762-4c98-b643-34c76e842343
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbe1c8932c082ce537cd5dc3f2b12d98c05c3811
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157993"
---
# <a name="dimension-types"></a>维度类型
  `Type` 属性设置为服务器和客户端应用程序提供有关维度内容的信息。 在某些情况下，`Type` 设置只为客户端应用程序提供指导信息，并且为可选项。 在其他情况下，例如 `Accounts` 维度或 `Time` 维度，维度及其特性的 `Type` 属性设置可以确定基于服务器的特定行为，并且实现多维数据集中的某些行为也可能需要该属性设置。 例如，维度的 `Type` 属性可以设置为 `Accounts`，从而向客户端应用程序指示标准维度包含帐户特性。 有关时间、 帐户和货币维度的详细信息，请参阅[创建日期类型维度](../multidimensional-models/database-dimensions-create-a-date-type-dimension.md)，[创建父子类型维度的财务帐户](../multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)，和[创建一种货币键入维度](../multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)。  
  
 维度类型的默认设置为 `Regular`，该设置不对维度内容进行任何假设。 当您初始定义维度时，该设置为所有维度的默认设置，除非您在使用维度向导定义维度时指定了 `Time`。 如果维度向导没有为维度类型列出合适的类型，则还应当将 `Regular` 继续用做维度类型。  
  
## <a name="available-dimension-types"></a>可用维度类型  
 下表描述了中可用的维度类型[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
|维度类型|Description|  
|--------------------|-----------------|  
|Regular|一种其类型尚未被设置为特殊维度类型的维度。|  
|Time|一种其属性表示时间段（如年、半期、季度、月和天）的维度。|  
|Organization|一种其属性表示单位信息（如雇员或分公司）的维度。|  
|Geography|一种其属性表示地域信息（如市县或邮政编码）的维度。|  
|BillOfMaterials|一种其属性表示库存或制造信息（如产品的部件列表）的维度。|  
|帐户|一种其属性表示用于财务报表用途的科目表的维度。|  
|Customers|一种其属性表示客户信息或联系信息的维度。|  
|Products|一种其属性表示产品信息的维度。|  
|应用场景|一种其属性表示计划或策略分析信息的维度。|  
|Quantitative|一种其属性表示定量信息的维度。|  
|实用工具|一种其属性表示杂项信息的维度。|  
|货币|该类型的维度包含货币数据和元数据。|  
|Rates|一种其属性表示货币汇率信息的维度。|  
|Channel|一种其属性表示渠道信息的维度。|  
|Promotion|一种其属性表示营销促销信息的维度。|  
  
## <a name="see-also"></a>请参阅  
 [使用现有表创建维度](../multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [维度（Analysis Services - 多维数据）](dimensions-analysis-services-multidimensional-data.md)  
  
  
