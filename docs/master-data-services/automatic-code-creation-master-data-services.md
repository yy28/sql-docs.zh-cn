---
title: "自动创建代码 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 9eba993695071796b6f9a4dfb4b05a1d1382be5a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="automatic-code-creation-master-data-services"></a>自动创建代码 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，可以为 Code 属性或任何其他数值属性自动生成数值。 自动生成代码时，不会阻止您输入其他代码值；实际上只是自动设置初始值。  
  
## <a name="generating-code-values"></a>生成 Code 值  
 管理员可以通过编辑关联实体的属性，为 Code 属性配置自动生成的值。 他们可以指定一个初始值，让每个后续值依次增加 1。  
  
 在相关工具之一中或使用临时过程向 MDS 中输入 Code 值时，可以保留 Code 值为空，Code 值将自动生成。 也可以指定您选择的 Code 值。  
  
## <a name="generating-other-attribute-values"></a>生成其他属性值  
 管理员可以通过创建业务规则，自动为 Code 之外的属性生成值。 他们可以指定一个初始值，然后指定每个后续值按其递增的值。  
  
 在相关工具之一中或使用临时过程向 MDS 中输入属性值时，可以保留属性值为空。 应用业务规则时，将以最大的现有值为基础增加值。 例如，如果您的规则是“属性默认为一个从 1 开始、增量为 4 的生成值”，并且属性当前的最大值是 700，则添加的下一个成员的值将是 704。  
  
## <a name="related-tasks"></a>相关任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|自动为 Code 属性生成值。|[自动生成 Code 属性值 (Master Data Services)](../master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|自动为其他属性生成值。|[自动生成 Code 之外的属性值 (Master Data Services)](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [Master Data Services 概述 (MDS)](../master-data-services/master-data-services-overview-mds.md)  
  
-   [业务规则 (Master Data Services)](../master-data-services/business-rules-master-data-services.md)  
  
-   [实体 (Master Data Services)](../master-data-services/entities-master-data-services.md)  
  
  

