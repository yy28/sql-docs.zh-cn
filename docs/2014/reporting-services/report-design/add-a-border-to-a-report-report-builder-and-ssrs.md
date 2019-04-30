---
title: 向报表添加边框（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 81412f94-2991-4e58-bc05-5ccc0cbf2a75
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1bb9deac03a2ba3683922a8c7e361cb908c787c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206905"
---
# <a name="add-a-border-to-a-report-report-builder-and-ssrs"></a>向报表添加边框（报表生成器和 SSRS）
  通过向表头、表尾和表体本身添加边框（而不是添加线条或矩形），可以为报表添加边框。  
  
 如果在表头和表尾上添加了报表边框，请不要在报表的第一页和最后一页禁用表头和表尾。 如果禁用了，那么报表的第一页和最后一页的顶部或底部的边框可能不完整。 有关详细信息，请参阅[页眉和页脚（报表生成器和 SSRS）](page-headers-and-footers-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-border-to-a-report"></a>向报表添加边框  
  
1.  右键单击页眉中任何项的外部，然后单击“页眉属性”。 在 **“边框”** 选项卡上，添加所需样式的左边框、上边框和右边框。  
  
    > [!NOTE]  
    >  如果不在报表中使用标头，然后就可以只是表体周围的边框或您可以添加从标头**插入**选项卡。  
  
2.  右键单击设计图面上任何项外部的主体，然后单击“主体属性”。 在 **“边框”** 选项卡上，添加所需样式的左边框和右边框。  
  
3.  右键单击页脚中任何项的外部，然后单击“页脚属性”。 在 **“边框”** 选项卡上，添加所需样式的左边框、下边框和右边框。  
  
## <a name="see-also"></a>请参阅  
 [矩形和线条（报表生成器和 SSRS）](rectangles-and-lines-report-builder-and-ssrs.md)  
  
  
