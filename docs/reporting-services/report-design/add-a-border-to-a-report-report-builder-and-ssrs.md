---
title: 向报表添加边框（报表生成器）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 81412f94-2991-4e58-bc05-5ccc0cbf2a75
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7790d44cc4160d7f61562cf470da43bb49a82cf2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080780"
---
# <a name="add-a-border-to-a-report-report-builder-and-ssrs"></a>向报表添加边框（报表生成器和 SSRS）
  通过向表头、表尾和表体本身添加边框（而不是添加线条或矩形），可以为 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表添加边框。    
    
 如果在表头和表尾上添加了报表边框，请不要在报表的第一页和最后一页禁用表头和表尾。 如果禁用了，那么报表的第一页和最后一页的顶部或底部的边框可能不完整。 有关详细信息，请参阅[页眉和页脚（报表生成器和 SSRS）](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)。    
    
## <a name="to-add-a-border-to-a-report"></a>向报表添加边框    
    
1.  右键单击页眉中任何项的外部，然后单击“页眉属性”  。 在 **“边框”** 选项卡上，添加所需样式的左边框、上边框和右边框。    
    
    > [!NOTE]    
    >  如果没有在报表中使用页眉，则可以仅围绕表体放置边框，也可以从“插入”选项卡中添加页眉  。    
    
2.  右键单击设计图面上任何项外部的主体，然后单击“主体属性”  。 在 **“边框”** 选项卡上，添加所需样式的左边框和右边框。    
    
3.  右键单击页脚中任何项的外部，然后单击“页脚属性”  。 在 **“边框”** 选项卡上，添加所需样式的左边框、下边框和右边框。    
    
## <a name="see-also"></a>另请参阅    
 [矩形和线条（报表生成器和 SSRS）](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)    
    
  
