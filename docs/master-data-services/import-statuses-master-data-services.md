---
title: 导入状态 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 306577c5-e7d7-4cff-aff4-efb5c6354036
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5a4860fac5035d7c24b552d11895842b78254f52
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="import-statuses-master-data-services"></a>导入状态 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 **“集成管理”** 功能区域中的 **“临时批处理”** 页上，以下状态可能会出现。  
  
|“登录属性”|Description|Status_ID|  
|------------|-----------------|----------------|  
|排队待运行|批处理尚未开始处理。|@shouldalert|  
|正在运行|批处理正在处理。|2|  
|已完成|批处理已完成处理。|3|  
|排队待清除|批处理已处理完毕，将被清除。|4|  
|已清除|批处理已清除。|5|  
  
## <a name="see-also"></a>另请参阅  
 [概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
  
