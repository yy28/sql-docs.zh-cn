---
title: 导入状态 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 306577c5-e7d7-4cff-aff4-efb5c6354036
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c3905312358c36688e4c20a5a78d6c5504c745aa
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404119"
---
# <a name="import-statuses-master-data-services"></a>导入状态 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 **“集成管理”** 功能区域中的 **“临时批处理”** 页上，以下状态可能会出现。  
  
|“登录属性”|描述|Status_ID|  
|------------|-----------------|----------------|  
|排队待运行|批处理尚未开始处理。|@shouldalert|  
|正在运行|批处理正在处理。|2|  
|已完成|批处理已完成处理。|3|  
|排队待清除|批处理已处理完毕，将被清除。|4|  
|已清除|批处理已清除。|5|  
  
## <a name="see-also"></a>另请参阅  
 [概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
  
