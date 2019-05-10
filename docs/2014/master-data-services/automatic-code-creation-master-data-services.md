---
title: 自动创建代码 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7ee7e06829f72ab44fd036766907be94c95b7d90
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483695"
---
# <a name="automatic-code-creation-master-data-services"></a>自动创建代码 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，可以为 Code 属性或任何其他数值属性自动生成数值。 自动生成代码时，不会阻止您输入其他代码值；实际上只是自动设置初始值。  
  
## <a name="generating-code-values"></a>生成 Code 值  
 管理员可以通过编辑关联实体的属性，为 Code 特性配置自动生成的值。 他们可以指定一个初始值，让每个后续值依次增加 1。  
  
 在相关工具之一中或使用临时过程向 MDS 中输入 Code 值时，可以保留 Code 值为空，Code 值将自动生成。 也可以指定您选择的 Code 值。  
  
## <a name="generating-other-attribute-values"></a>生成其他属性值  
 管理员可以通过创建业务规则，自动为 Code 之外的属性生成值。 他们可以指定一个初始值，然后指定每个后续值按其递增的值。  
  
 在相关工具之一中或使用临时过程向 MDS 中输入属性值时，可以保留属性值为空。 应用业务规则时，将以最大的现有值为基础增加值。 例如，如果规则是“属性默认为一个从 1 开始、增量为 4 的生成值”，并且属性当前的最大值是 700，则添加的下一个成员的值将是 704。  
  
## <a name="deleting-automatically-generated-values"></a>删除自动生成的值  
 在管理员启用为 Code 属性自动生成值之后，用户可能会意外删除具有要重复使用的 Code 值的成员。 将显示"成员代码已被某个已删除的成员使用"错误消息。 下面是两种可能的解决方案：  
  
-   在中**版本管理**功能区域中，管理员可以撤消删除成员时发生的事务。 但是，这意味着还原所有的前一个成员属性和层次结构和集合中的成员身份。 有关详细信息，请参阅[撤消事务&#40;Master Data Services&#41;](reverse-a-transaction-master-data-services.md)。  
  
-   管理员可以使用临时过程永久删除成员。 有关详细信息，请参阅[停用或通过使用临时过程删除成员&#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|自动为 Code 属性生成值。|[自动生成 Code 属性值 (Master Data Services)](../../2014/master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|自动为其他属性生成值。|[自动生成 Code 之外的属性值 (Master Data Services)](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [Master Data Services 概述](master-data-services-overview-mds.md)  
  
-   [业务规则 (Master Data Services)](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [实体 (Master Data Services)](../../2014/master-data-services/entities-master-data-services.md)  
  
  
