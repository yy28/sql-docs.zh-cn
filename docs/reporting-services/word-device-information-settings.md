---
title: "Word 设备信息设置 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 491940329df26ba67f447aacb6a32f5d6578c4a5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="word-device-information-settings"></a>Word 设备信息设置
  下表列出以 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 格式呈现时的设备信息设置。  
  
|设置|“值”|  
|-------------|-----------|  
|**AutoFit**|**False**。 自动调整对于任何 Word 表都设置为 **false** 。<br /><br /> **True**。 自动调整对于每个 Word 表都设置为 **true** 。<br /><br /> **Never**。 对任何 Word 表均未设置自动调整值并且行为还原为 Word 默认值。<br /><br /> **Default**。 自动调整设置于窄于每个逻辑页上物理绘图区（不包括边距的物理页宽）的表。|  
|**ExpandToggles**|指示可以滚动的所有项是否以其完全展开的状态呈现。 默认值是 **false**秒。|  
|**FixedPageWidth**|指示写入 DOC 文件的页宽是否将增大以适合表体中最大页的宽度。 默认值是 **false**秒。|  
|**OmitHyperlinks**|指示是否忽略对所有项的超链接操作（如果设置）。 默认值为 **false**。|  
|**OmitDrillthroughs**|指示是否忽略对所有项的钻取操作（如果设置）。 默认值为 **false**。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [自定义在 RSReportServer.Config 中的呈现扩展插件参数](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 &#40;SSRS &#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
