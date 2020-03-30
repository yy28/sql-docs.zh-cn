---
title: 设置同步作用域（报表生成器）| Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 6f4a11e6-6151-47be-a43f-e3dbf6c0e737
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b5c844bf2ad09ee29dbcda1773e20d93eeb069d1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081006"
---
# <a name="set-synchronization-scope-report-builder-and-ssrs"></a>设置同步作用域（报表生成器和 SSRS）
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，指示器通过同步指定范围内指示器值的范围，提供数据值。   
    
  默认情况下，作用域是指示器的父容器，例如包含指示器的表或矩阵。 您可以根据报表的布局，更改指示器的同步。 例如，如果表之类的数据区域具有某一行组，则您可以将该组指定为指示器作用域。 指示器还可以忽略同步。  
  
 可以通过使用表达式设置度量单位之类的选项。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
 有关了解和设置报表作用域的常规信息，请参阅[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="to-change-the-synchronization-scope-of-an-indicator"></a>更改指示器的同步作用域  
  
1.  右键单击要更改的指示器，然后单击“指示器属性”  。  
  
2.  在左窗格中单击 **“值和状态”** 。  
  
3.  在 **“同步作用域”** 列表中，单击要应用的作用域。  
  
     从指示器中删除同步作用域的“(无)”选项始终可用  。 其他选项取决于您的报表布局。  
  
     或者，单击“表达式”(fx) 按钮以编辑设置作用域的表达式   。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [指示器（报表生成器和 SSRS）](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
