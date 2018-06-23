---
title: Word 设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 5b31b3c3ea0cf5b70967ca099e0b979f0c929334
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123541"
---
# <a name="word-device-information-settings"></a>Word 设备信息设置
  下表列出以 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 格式呈现时的设备信息设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|`AutoFit`|`False`的用户。 自动调整设置为`false`在任何 Word 表上设置。<br /><br /> `True`的用户。 自动调整对于每个 Word 表都设置为 `true`。<br /><br /> `Never`的用户。 对任何 Word 表均未设置自动调整值并且行为还原为 Word 默认值。<br /><br /> `Default`的用户。 自动调整设置于窄于每个逻辑页上物理绘图区（不包括边距的物理页宽）的表。|  
|`ExpandToggles`|指示可以滚动的所有项是否以其完全展开的状态呈现。 默认值是 `false`。|  
|`FixedPageWidth`|指示写入 DOC 文件的页宽是否将增大以适合表体中最大页的宽度。 默认值是 `false`。|  
|**OmitHyperlinks**|指示是否忽略对所有项的超链接操作（如果设置）。 默认值为 `false`|  
|`OmitDrillthroughs`|指示是否忽略对所有项的钻取操作（如果设置）。 默认值为 `false`|  
  
## <a name="see-also"></a>请参阅  
 [将设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  