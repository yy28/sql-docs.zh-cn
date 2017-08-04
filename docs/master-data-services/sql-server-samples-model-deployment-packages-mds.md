---
title: "SQL Server 示例： 模型部署包 (MDS) |Microsoft 文档"
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- master data services
- sample
ms.assetid: 9b31b7b6-319b-4840-b67d-eb383e7762b1
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7a031ba18c6782cdd73ae31ef395bc2ecdcf102
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>SQL Server 示例： 模型部署包 (MDS)
  安装 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]时，包含使用数据的示例模型包。 默认位置的这些包文件是\<驱动器 > files\microsoft SQL Server\130\Master 数据 Services\Samples\Packages。  
  
 有关如何部署示例模型包的说明，请参阅 [部署示例模型和数据](../master-data-services/master-data-services-installation-and-configuration.md#deploySample)。 可以使用 [MDSModelDeploy 工具](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)部署示例模型包。  
  
> [!IMPORTANT]  
>  **中的示例更新[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
>   
>  示例包已更新为支持以下新功能。  
>   
>  -   显示多对多关系。  
>   
>      有关详细信息，请参阅 [示例模型中的 M2M 关系](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md#M2MSample)。  

> -   限制基于域的属性的允许值。  
>   
>      有关详细信息，请参阅[创建基于域的属性 (Master Data Services)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)。  
> -   针对实体更改的需要批准。  
>   
>      有关详细信息，请参阅[需要审批 (Master Data Services)](../master-data-services/approval-required-master-data-services.md)。  
> -   在业务规则中使用 Not 和 Else 运算符  
>   
>      有关详细信息，请参阅 [业务规则示例](../master-data-services/business-rule-examples-master-data-services.md)。  
> -   实现自定义索引  
>   
>      有关详细信息，请参阅[自定义索引 (Master Data Services)](../master-data-services/custom-index-master-data-services.md)。  
 

 
 在 Master Data Services，包是包含可部署模型结构和 （可选） 模型中的数据的 XML 文件。 使用模型包可以将模型的副本从一个 MDS 环境移到另一个环境，或者在现有的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 环境中创建新模型。  
  
## <a name="see-also"></a>另请参阅  
 [使用 MDSModelDeploy 部署模型部署包](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  

