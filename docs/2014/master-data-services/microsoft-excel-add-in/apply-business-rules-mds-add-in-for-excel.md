---
title: 应用业务规则 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9f1db21079b7c07394a149b173195ed8fca56d5e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254739"
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>应用业务规则（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中，如果需要验证数据并确认其有效，可应用业务规则。 您可以更正验证结果并重新发布数据。  
  
> [!NOTE]  
>  发布数据时会自动验证数据。 有关详细信息，请参阅[验证存储过程 (Master Data Services)](../validation-stored-procedure-master-data-services.md)。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“资源管理器”** 功能区域。  
  
-   必须具有包含 MDS 管理的数据的活动工作表。  
  
### <a name="to-apply-business-rules"></a>应用业务规则  
  
1.  在 **“发布并验证”** 组中，单击 **“应用规则”**。  
  
    > [!NOTE]  
    >  一次验证的成员（行）的数目取决于 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]中的设置。 有关详细信息，请参阅 [Business Rule Settings](../system-settings-master-data-services.md#BusinessRules)。  
  
2.  根据业务规则对数据进行验证后，将显示两个状态列。 如果不自动显示这些列，请在 **“发布并验证”** 组中，单击 **“显示状态”** 以查看这些列。  
  
## <a name="see-also"></a>请参阅  
 [发布数据&#40;MDS add-in for Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
