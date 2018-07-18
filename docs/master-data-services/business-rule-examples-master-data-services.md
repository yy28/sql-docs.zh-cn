---
title: 业务规则示例 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3974b9be-4b7c-4a37-ab26-1a36ef455744
caps.latest.revision: 21
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 60fdefca0b30606ce6cb11ab8cd44f05188b59f6
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35335331"
---
# <a name="business-rule-examples-master-data-services"></a>业务规则示例 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文演示 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]的业务规则示例。 你会在 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]安装附带的示例模型中找到这些示例。   
  
有关如何部署示例模型的说明，请参阅 [Master Data Services 的安装和配置](../master-data-services/master-data-services-installation-and-configuration.md)。  
  
  
## <a name="business-rule-examples"></a>业务规则示例  
示例模型 |实体  |业务规则名称| 描述  
---------|---------|---------|-----------|  
Customer    | Customer   | Person pmt terms| 为客户指定默认付款条款。          
在下面的业务规则中，如果 CustomerType 属性值满足 `is equal` [规则条件](../master-data-services/business-rule-conditions-master-data-services.md)，则 `defaults to` [规则操作](../master-data-services/business-rule-conditions-master-data-services.md) 会应用于 PaymentTerms 属性。 否则不执行任何操作。  
```  
If  
    CustomerType is equal to 2  
Then  
    PaymentTerms defaults to CASH  
Else  
    None      
```  
  
**--------------------------------------------------**  
  
示例模型  |实体  |业务规则名称|描述    
---------|---------|---------|---------------  
Customer     | Customer    | Org pmt terms | 为组织指定默认付款条款。         
在下面的业务规则中，如果 CustomerType 属性值满足 `is equal` [规则条件](../master-data-services/business-rule-conditions-master-data-services.md)，则 `defaults to` [规则操作](../master-data-services/business-rule-actions-master-data-services.md) 会应用于 PaymentTerms 属性。 否则不执行任何操作。  
```  
If  
    CustomerType is equal to 1  
Then  
    PaymentTerms defaults to 210Net30  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
示例模型  |实体  |业务规则名称| 描述    
---------|---------|---------|-----------  
Product     |  Product       | DaysToManufacture |为内部制造指定制造天数范围。          
在下面的业务规则中，如果 InHouseManufacture 属性值满足 `is equal` [规则条件](../master-data-services/business-rule-conditions-master-data-services.md)，则 `must be between` [规则操作](../master-data-services/business-rule-actions-master-data-services.md) 会应用于 DaysToManufacture 属性。 否则不执行任何操作。  
```  
If  
    InHouseManufacture is equal to Y  
Then  
    DaysToManufacture must be between 1 and 10  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
示例模型  |实体  |业务规则名称|描述    
---------|---------|---------|-------------  
Product     |Product         |Required fields| 为产品实体成员指定必需属性。           
在下面的业务规则中，在所有情况下都会为指定属性执行 `is required` [验证操作](../master-data-services/business-rule-actions-master-data-services.md) 。 属性值不能为 Null 或空白。  
```  
If  
    None  
Then  
    Name is required  
    ProductSubCategory is required  
    Color is required  
    StandardCost is required  
    SafetyStockLevel is required  
    ReorderPoint is required  
    InHouseManufacture is required  
    SellStartDate is required  
    FinishedGoodIndicator is required  
    ProductLine is required  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
示例模型  |实体  |业务规则名称|描述    
---------|---------|---------|-----------  
Product     | Product        |  Std Cost| 要求标准成本大于 0。        
在下面的业务规则中，在所有情况下都会将 `must be greater than` [规则操作](../master-data-services/business-rule-actions-master-data-services.md) 应用于产品的 StandardCost 属性。  
```  
If  
    None  
Then  
    StandardCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
示例模型  |实体  |业务规则名称|描述    
---------|---------|---------|------------  
Product     | Product        | FG MSRP Cost|指定产品是否为产成品，并且 MSRP（制造商建议零售价）和经销商成本必须大于 0。           
  
在下面的业务规则中，如果 FinishedGoodIndicator 属性值满足 `is equal` [规则条件](../master-data-services/business-rule-conditions-master-data-services.md)，则 `must be greater than` [规则操作](../master-data-services/business-rule-actions-master-data-services.md) 会应用于 MSRP 和 DealerCost 属性。  
```  
If  
    FinishedGoodIndicator is equal to Y  
Then  
    MSRP must be greater than 0  
    DealerCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
示例模型  |实体  |业务规则名称|描述    
---------|---------|---------|------------  
Product     | Product        |  Default Name| 基于 Color 和 Class 属性的值指定默认产品名称。 当 Color 属性值不是 YLO 并且 Class 属性不是 NA 时，默认名称是 Yellow NA。         
在下面的业务规则中，如果 Color 和 Class 属性不满足 `is equal` 规则条件，则 `defaults to` [规则操作](../master-data-services/business-rule-actions-master-data-services.md) 会应用于 Name 属性。  
```  
If  
    (Color is equal to YLO AND Class is equal to NA) is not true  
Then  
    Name defaults to Yellow NA  
Else  
    Name defaults to Other  
```  
  
**--------------------------------------------------**  
  
  
**在示例模型中查看业务规则示例**  
1. 导航在安装 MDS 之后设置的 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 网站，然后单击“系统管理”框。   
有关设置 Web 站点的说明，请参阅 [Master Data Services 的安装和配置](../master-data-services/master-data-services-installation-and-configuration.md)。  
2. 单击包含业务规则的示例模型（如以上表所列），然后单击“实体”。  
3. 单击应用规则的实体（如以下表所列），然后单击“业务规则”。  
4. 单击要查看的业务规则的名称。 UI 将展开，以显示 **If**、 **Then** 和 **Else** 语句。  
  
 
  
  
  
  

