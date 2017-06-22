---
title: "向报表 （报表生成器和 SSRS） 添加边框 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 81412f94-2991-4e58-bc05-5ccc0cbf2a75
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 824ca565b87a77add1c547aafb264345a9a63dab
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="add-a-border-to-a-report-report-builder-and-ssrs"></a>向报表添加边框（报表生成器和 SSRS）
  通过向表头、表尾和表体本身添加边框（而不是添加线条或矩形），可以为 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表添加边框。    
    
 如果在表头和表尾上添加了报表边框，请不要在报表的第一页和最后一页禁用表头和表尾。 如果禁用了，那么报表的第一页和最后一页的顶部或底部的边框可能不完整。 有关详细信息，请参阅[页眉和页脚（报表生成器和 SSRS）](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)。    
    
## <a name="to-add-a-border-to-a-report"></a>向报表添加边框    
    
1.  在表头中任何项外部的表头中右键单击，然后单击“表头属性”。 在 **“边框”** 选项卡上，添加所需样式的左边框、上边框和右边框。    
    
    > [!NOTE]    
    >  如果没有在报表中使用表头，则可以仅围绕表体放置边框，也可以从“插入”选项卡中添加表头。    
    
2.  在设计图面上任何项外部的主体中右键单击，然后单击“主体属性”。 在 **“边框”** 选项卡上，添加所需样式的左边框和右边框。    
    
3.  在表尾中任何项外部的表尾中右键单击，然后单击“表尾属性”。 在 **“边框”** 选项卡上，添加所需样式的左边框、下边框和右边框。    
    
## <a name="see-also"></a>另请参阅    
 [矩形和线条（报表生成器和 SSRS）](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)    
    
  
