---
title: 更改跟踪 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- change tracking [SQL Server]
ms.assetid: 5e879c65-0d38-454f-9a20-62a6e72c89f7
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: fb6760d737656b0c8fedb82b315d45e59152de79
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024604"
---
# <a name="change-tracking-master-data-services"></a>更改跟踪 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以使用更改跟踪组在属性值发生更改时执行操作。 如果您不知道新值是什么，但想要知道是否有任何更改发生，则使用更改跟踪。  
  
## <a name="configuring-change-tracking"></a>配置更改跟踪  
 若要配置更改跟踪，请向更改跟踪组添加属性。 该组可以包含一个或多个属性。 然后，创建业务规则以定义在该组中任何属性发生更改时执行的操作。  
  
> [!NOTE]  
>  更改跟踪业务规则认为临时（导入）数据将发生更改。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|向更改跟踪组添加属性。|[向更改跟踪组添加属性&#40;Master Data Services&#41;](add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|创建业务规则以便基于属性更改启动操作。|[基于属性值更改启动操作&#40;Master Data Services&#41;](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [验证&#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md)  
  
-   [业务规则&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [属性&#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  