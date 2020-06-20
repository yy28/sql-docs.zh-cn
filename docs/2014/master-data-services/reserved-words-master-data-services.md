---
title: 保留字 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cd1e5bcee01992607cf9bffca1a72dd99bd75fbe
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960577"
---
# <a name="reserved-words-master-data-services"></a>保留字 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当您创建模型对象或成员时，不能使用某些字词。 使用这些字词可能导致错误。  
  
> [!NOTE]  
>  您还应限制使用特殊字符（符号、连字符等）。  
  
-   [模型](#models)  
  
-   [实体](#entities)  
  
-   [显式层次结构](#exhierarchies)  
  
-   [属性](#attributes)  
  
-   [成员](#members)  
  
##  <a name="models"></a><a name="models"></a>机型  
 如果创建的模型的名称设置为 "**名称**"，请不要选择 "**使用与模型相同的名称创建实体**"，因为**名称**不能用于实体名称。  
  
##  <a name="entities"></a><a name="entities"></a>条目  
 对于实体名称，不能使用 **Name** 或 **Code**。  
  
##  <a name="explicit-hierarchies"></a><a name="exhierarchies"></a>显式层次结构  
 对于显式层次结构名称，不能使用 **Name** 或 **Code**。  
  
##  <a name="attributes"></a><a name="attributes"></a>属性  
  
-   **ID**  
  
-   **代码**  
  
-   **名称**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a><a name="members"></a>组员  
 对于成员，不能对**Code**属性值使用**MDMMemberStatus**或**ROOT** 。  
  
## <a name="see-also"></a>另请参阅  
 [Master Data Services 概述](master-data-services-overview-mds.md)  
  
  
