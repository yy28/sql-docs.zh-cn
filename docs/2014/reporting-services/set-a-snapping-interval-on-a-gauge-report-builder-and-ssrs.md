---
title: 在仪表上设置对齐间隔（报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0ece7297-6e2f-47fb-835d-b9e9cce53fe2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e2a35e4d6fefb6830774ffd7b2c3bc13a5e097c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101369"
---
# <a name="set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs"></a>在仪表上设置对齐间隔（报表生成器和 SSRS）
  对齐间隔定义一个数值，舍入后的值是它的倍数。 默认情况下，仪表将指向已在数据窗格中指定的字段的精确值。 但是，您可能希望该精确值向上舍入或向下舍入，以便指针与预设的间隔对齐。 例如，如果仪表上的值为 34.2 并且您将对齐间隔指定为 5，则仪表指针将指向 35。 如果仪表上的值为 31.2 并且您将对齐间隔指定为 5，则仪表指针将指向 30。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-snapping-interval-on-a-gauge"></a>在仪表上设置对齐间隔  
  
1.  单击仪表上的任意数字，以突出显示刻度。  
  
2.  打开“属性”窗格。  
  
    > [!NOTE]  
    >  如果看不到 "属性" 窗格，请单击 "**查看**" 选项卡，然后选中 "**属性**" 复选框。  
  
3.  在 "**指针**" 属性中，单击 "（...）" 按钮。 此时将打开指针集合编辑器。  
  
4.  将**SnappingEnabled**属性设置为`True`。  
  
5.  将**SnappingInterval**设置为一个表示对齐间隔的值。 指针将与已指定的值的最接近舍入倍数对齐。  
  
## <a name="see-also"></a>另请参阅  
 [设置仪表上刻度的格式 &#40;报表生成器和 SSRS&#41;](report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [设置仪表上的指针格式 &#40;报表生成器和 SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [仪表（报表生成器和 SSRS）](report-design/gauges-report-builder-and-ssrs.md)  
  
  
