---
title: 保留字
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 817e15d2fe7e91f63628826f58d6a86dd4edbcb3
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727916"
---
# <a name="reserved-words-master-data-services"></a>保留字 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当您创建模型对象或成员时，不能使用某些字词。 使用这些字词可能导致错误。  
  
> [!NOTE]  
>  您还应限制使用特殊字符（符号、连字符等）。  
  
-   [Models](../master-data-services/reserved-words-master-data-services.md#models)  
  
-   [实体](../master-data-services/reserved-words-master-data-services.md#entities)  
  
-   [显式层次结构](../master-data-services/reserved-words-master-data-services.md#exhierarchies)  
  
-   [属性](../master-data-services/reserved-words-master-data-services.md#attributes)  
  
-   [成员](../master-data-services/reserved-words-master-data-services.md#members)  
  
##  <a name="models"></a> Models  
 如果你创建名称设置为 **Name** 或 **Code**的模型，则不要选择“使用与模型相同的名称创建实体”，因为 **Name** 或 **Code** 不能用于实体名称。  
  
##  <a name="entities"></a> 实体  
 对于实体名称，不能使用 **Name** 或 **Code**。  
  
##  <a name="exhierarchies"></a> 显式层次结构  
 对于显式层次结构名称，不能使用 **Name** 或 **Code**。  
  
##  <a name="attributes"></a> 属性  
  
-   **ID**  
  
-   **代码**  
  
-   **EnterUserName**  
  
-   **LastChgUserName**  
  
-   **名称**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> 成员  
 对于成员，不能对 **Code**属性值使用 **MDMMemberStatus**、 **MDMUnused** 或 **ROOT** 。  
  
## <a name="see-also"></a>另请参阅  
 [Master Data Services 概述 (MDS)](../master-data-services/master-data-services-overview-mds.md)  
  
  
