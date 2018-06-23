---
title: 图表故障排除（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: b5369ef0fd3f96345e0fc7e0c688f1230bfe41c1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123560"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>图表故障排除（报表生成器和 SSRS）
  对以下问题的解答可能在您使用图表时对您有所帮助。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>为什么我的图表对值轴上的值进行计数，而不是求和？  
 大多数图表类型都要求数值放置在通常作为 y 轴的值轴上，以便能够正确地绘制图表。 如果值字段的数据类型是`String`，图表将无法显示数值，即使在字段中有数字。 相反，该图表将显示包含该字段中值的行的总行数。 若要避免出现此情况，请确保用于值序列的字段是数字数据类型的，而不是包含格式化数字的字符串。  
  
## <a name="see-also"></a>请参阅  
 [图表&#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  