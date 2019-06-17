---
title: 维度类型 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 663c26ac169c11e5ab2d9b90285419cf4145368c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025771"
---
# <a name="database-dimension-properties---types"></a>数据库维度属性 - 类型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  **类型**属性设置可以提供有关内容的维度与服务器和客户端应用程序的信息。 在某些情况下，**类型**设置只为客户端应用程序提供指导和是可选的。 在其他情况下，如**帐户**或**时间**维度**类型**维度及其特性的属性设置确定特定的基于服务器的行为可能需要在多维数据集中实现某些行为。 例如，**类型**维度的属性可以设置为**帐户**向客户端应用程序指示标准维度包含帐户特性。 有关时间、 帐户和货币维度的详细信息，请参阅[创建日期类型维度](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)，[创建父子类型维度的财务帐户](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)，和[创建一种货币键入维度](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)。  
  
 维度类型的默认设置**正则**，这不会假设即将内容的维度。 这是所有维度的默认设置，除非您指定的初始定义维度时**时间**时定义维度使用维度向导。 此外应将保留**正则**作为维度类型，如果维度向导不会列出维度类型的适当的类型。  
  
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
|Currency|该类型的维度包含货币数据和元数据。|  
|Rates|一种其属性表示货币汇率信息的维度。|  
|Channel|一种其属性表示渠道信息的维度。|  
|Promotion|一种其属性表示营销促销信息的维度。|  
  
## <a name="see-also"></a>请参阅  
 [使用现有表创建维度](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [维度（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
