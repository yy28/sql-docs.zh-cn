---
title: 更改跟踪 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server]
ms.assetid: 5e879c65-0d38-454f-9a20-62a6e72c89f7
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7b4b7d9d9d153456ca471196c6480465d057e412
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483524"
---
# <a name="change-tracking-master-data-services"></a>更改跟踪 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以使用更改跟踪组在属性值发生更改时执行操作。 如果不知道新值是什么，但想要知道是否发生了任何更改，则使用更改跟踪。  
  
## <a name="configuring-change-tracking"></a>配置更改跟踪  
 若要配置更改跟踪，请向更改跟踪组添加属性。 该组可以包含一个或多个属性。 然后，创建业务规则以定义在该组中任何属性发生更改时执行的操作。  
  
> [!NOTE]  
>  更改跟踪业务规则认为临时（导入）数据将发生更改。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|向更改跟踪组添加属性。|[向更改跟踪组添加属性 (Master Data Services)](add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|创建业务规则以便基于属性更改启动操作。|[基于属性值更改启动操作 (Master Data Services)](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [验证 (Master Data Services)](../../2014/master-data-services/validation-master-data-services.md)  
  
-   [业务规则 (Master Data Services)](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [属性 (Master Data Services)](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
