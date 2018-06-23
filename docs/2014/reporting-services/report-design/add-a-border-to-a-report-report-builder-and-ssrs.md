---
title: 向报表添加边框（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81412f94-2991-4e58-bc05-5ccc0cbf2a75
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 4295a712f277047c4e205d83c44bbc0ff444db32
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129618"
---
# <a name="add-a-border-to-a-report-report-builder-and-ssrs"></a>向报表添加边框（报表生成器和 SSRS）
  通过向表头、表尾和表体本身添加边框（而不是添加线条或矩形），可以为报表添加边框。  
  
 如果在表头和表尾上添加了报表边框，请不要在报表的第一页和最后一页禁用表头和表尾。 如果禁用了，那么报表的第一页和最后一页的顶部或底部的边框可能不完整。 有关详细信息，请参阅[页眉和页脚（报表生成器和 SSRS）](page-headers-and-footers-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-border-to-a-report"></a>向报表添加边框  
  
1.  右键单击页眉中任何项的外部，然后单击“页眉属性”。 在 **“边框”** 选项卡上，添加所需样式的左边框、上边框和右边框。  
  
    > [!NOTE]  
    >  如果不在报表中使用标头，你可以添加边框只是报表正文中，或者您可以添加标头的**插入**选项卡。  
  
2.  右键单击设计图面上任何项外部的主体，然后单击“主体属性”。 在 **“边框”** 选项卡上，添加所需样式的左边框和右边框。  
  
3.  右键单击页脚中任何项的外部，然后单击“页脚属性”。 在 **“边框”** 选项卡上，添加所需样式的左边框、下边框和右边框。  
  
## <a name="see-also"></a>请参阅  
 [矩形和线条&#40;报表生成器和 SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md)  
  
  