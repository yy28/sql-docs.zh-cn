---
title: "维度类型 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
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
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6484d74f95da6f17f2ff46554c5ca16fac38fc0a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="database-dimension-properties---types"></a>数据库维度属性的类型
  **类型**属性设置可以提供的服务器和客户端应用程序到维度内容的相关信息。 在某些情况下，**类型**仅提供客户端应用程序的指南，是可选的设置。 在其他情况下，如**帐户**或**时间**维度，**类型**属性设置为维度及其属性确定特定的基于服务器的行为并且可能需要实现的多维数据集中的某些行为。 例如，**类型**维度的属性可以设置为**帐户**以指示客户端应用程序的标准维度包含帐户属性。 有关时间、 帐户和货币维度的详细信息，请参阅[创建日期类型维度](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)，[创建父-子类型维度的财务帐户](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)，和[创建一种货币键入维度](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)。  
  
 维度类型的默认设置**正则**，这使得内容的相关维度的任何假设。 这是所有维度的默认设置，除非另行指定，最初定义维度时**时间**时定义使用维度向导的维度。 您还应该保留**正则**作为维度类型，如果维度向导未列出适当类型的维度类型。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [通过使用现有表创建维度](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [维度（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
