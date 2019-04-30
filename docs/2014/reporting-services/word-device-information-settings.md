---
title: Word 设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 628b9775ecd7fa23a7f63f0738b5c39c5cca2d5b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206279"
---
# <a name="word-device-information-settings"></a>Word 设备信息设置
  下表列出以 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 格式呈现时的设备信息设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|`AutoFit`|`False`。 自动调整对于任何 Word 表都设置为 `false`。<br /><br /> `True`。 自动调整对于每个 Word 表都设置为 `true`。<br /><br /> `Never`。 对任何 Word 表均未设置自动调整值并且行为还原为 Word 默认值。<br /><br /> `Default`。 自动调整设置于窄于每个逻辑页上物理绘图区（不包括边距的物理页宽）的表。|  
|`ExpandToggles`|指示可以滚动的所有项是否以其完全展开的状态呈现。 默认值为 `false`。|  
|`FixedPageWidth`|指示写入 DOC 文件的页宽是否将增大以适合表体中最大页的宽度。 默认值是 `false`。|  
|**OmitHyperlinks**|指示是否忽略对所有项的超链接操作（如果设置）。 默认值为 `false`|  
|`OmitDrillthroughs`|指示是否忽略对所有项的钻取操作（如果设置）。 默认值为 `false`|  
  
## <a name="see-also"></a>请参阅  
 [将设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
