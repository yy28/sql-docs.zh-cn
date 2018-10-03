---
title: 历史属性选项（渐变维度向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.histattriboption.f1
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3b2a0b30329516a478e07eeaddf4d04f6f5d8c65
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103618"
---
# <a name="historical-attribute-options-slowly-changing-dimension-wizard"></a>历史属性选项（渐变维度向导）
  可以使用 **“历史属性选项”** 对话框按开始日期和结束日期显示历史属性，或者将历史属性记录到专门的列中。  
  
 若要了解有关此向导的详细信息，请参阅 [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md)。  
  
## <a name="options"></a>选项  
 **使用单独的列显示当前和过期记录**  
 如果您选择使用单独的列来记录历史属性的状态，则下列选项可用：  
  
|选项|Description|  
|------------|-----------------|  
|**指示当前记录的列**|选择一个要在其中指示当前记录的列。|  
|**表示当前记录的值**|使用 **True** 或 **“当前”** 来显示该记录是否为当前记录。|  
|**表示过期记录的值**|使用 **False** 或 **“过期”** 来显示该记录是否为历史值。|  
  
 **使用开始日期和结束日期确定当前记录和过期记录**  
 此选项的维度表必须包括一个日期列。 如果您选择按开始日期和结束日期显示历史属性，则下列选项可用：  
  
|选项|Description|  
|------------|-----------------|  
|**开始日期列**|在维度表中选择要包含开始日期的列。|  
|**结束日期列**|在维度表中选择要包含结束日期的列。|  
|**用来设置日期值的变量**|从该列表中选择日期变量。|  
  
## <a name="see-also"></a>请参阅  
 [使用渐变维度向导配置输出](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
