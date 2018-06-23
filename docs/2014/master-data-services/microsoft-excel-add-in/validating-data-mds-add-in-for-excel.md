---
title: 验证数据 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71eda98f-01a4-4fff-8246-be3133782523
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 17a963b4ef2342e7c97069ce2ed7f5bd9eec6cd6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026352"
---
# <a name="validating-data-mds-add-in-for-excel"></a>验证数据（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，当你发布数据时，将进行两种类型的验证：  
  
-   任何已定义的业务规则将应用于数据。  
  
-   根据允许的属性值（例如，字符数或数据类型）对数据进行检查。  
  
 在每种情况下，有效数据都发布到 MDS 存储库中。 无效数据将被突出显示，并且错误的详细信息可能会显示在状态列中。  
  
## <a name="when-validation-occurs"></a>在发生验证时  
 在[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]，当您发布新的或更改数据，或手动应用业务规则时，将执行验证。  
  
 在业务规则失败时，数据仍发布到 MDS 存储库中。 在输入验证失败时，数据将不会发布到该存储库。  
  
## <a name="validation-statuses"></a>验证状态  
 在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，以下验证状态是可能的。  
  
|“登录属性”|Description|  
|------------|-----------------|  
|错误|行中的一个或多个值未通过针对 MDS 管理员定义的业务规则的验证。|  
|未验证|行中的值尚未根据业务规则进行验证。|  
|成功|行中的所有值都已根据业务规则通过了验证。|  
  
## <a name="input-statuses"></a>输入状态  
 在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，以下输入状态是可能的  
  
|“登录属性”|Description|  
|------------|-----------------|  
|错误|行中的一个或多个值不符合长度或数据类型之类的系统要求。 值在 MDS 存储库中不更新。|  
|新行|该行中的值尚未发布到 MDS 存储库中。|  
|只读|登录用户对该行中的一个或多个值具有只读权限，并且这些值不能更新。|  
|不变|行中没有任何值在工作表中进行了更改。 这并不意味着存储库中的值已更改；若要获取工作表中的最新数据，请在 **“连接并加载”** 组中单击 **“加载或刷新”**。<br /><br /> 这是每一行的默认设置。|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|确定哪些值未通过定义的业务规则。|[应用业务规则&#40;MDS add-in for Excel&#41;](apply-business-rules-mds-add-in-for-excel.md)|  
|为了帮助纠正验证错误，请查看某一成员发生的所有事务。|[查看成员的所有批注或事务（用于 Excel 的 MDS 外接程序）](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [将数据发布&#40;MDS add-in for Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  