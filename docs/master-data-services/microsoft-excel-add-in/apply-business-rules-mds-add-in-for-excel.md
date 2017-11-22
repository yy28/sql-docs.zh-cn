---
title: "应用业务规则 (MDS Add-in for Excel) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a1bf1f9c1c5ee2c30d9d550452e25d8742f81d0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>应用业务规则（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中，如果需要验证数据并确认其有效，可应用业务规则。 您可以更正验证结果并重新发布数据。  
  
> [!NOTE]  
>  发布数据时会自动验证数据。 有关详细信息，请参阅[验证 (Master Data Services)](../../master-data-services/validation-master-data-services.md)。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“资源管理器”** 功能区域。  
  
-   必须具有包含 MDS 管理的数据的活动工作表。  
  
### <a name="to-apply-business-rules"></a>应用业务规则  
  
1.  在 **“发布并验证”** 组中，单击 **“应用规则”**。  
  
    > [!NOTE]  
    >  一次验证的成员（行）的数目取决于 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]中的设置。 有关详细信息，请参阅 [Business Rule Settings](../../master-data-services/system-settings-master-data-services.md#BusinessRules)。  
  
2.  根据业务规则对数据进行验证后，将显示两个状态列。 如果不自动显示这些列，请在 **“发布并验证”** 组中，单击 **“显示状态”** 以查看这些列。  
  
## <a name="see-also"></a>另请参阅  
 [概述：从 Excel 导入数据（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
