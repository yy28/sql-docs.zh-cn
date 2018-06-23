---
title: 将报表链接到作为点击链接型报表模型 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- customizing clickthrough reports
- clickthrough reports, customizing
- clickthrough reports, templates
ms.assetid: 3af42de3-67ef-41c2-bc8a-7045baec6f63
caps.latest.revision: 26
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 9dfe16933e0c2b335cf68816113c336561aac1ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128024"
---
# <a name="link-a-report-to-a-model-as-a-clickthrough-report"></a>将报表作为点击链接型报表链接到模型
  您可以不使用默认的点击链接型报表模板，而创建报表生成器报表并将其链接到报表模型中的特定实体。 当查看报表的用户单击主报表中的交互式数据时，该报表便会显示为点击链接型报表。 若要将报表链接到实体，使用[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]报表管理器。  
  
> [!IMPORTANT]  
>  报表中使用的主实体（或基实体）必须与报表所链接到的实体相同。  
  
### <a name="to-start-report-manager-from-a-browser"></a>从浏览器启动报表管理器  
  
1.  打开[!INCLUDE[msCoName](../includes/msconame-md.md)]Internet Explorer 6.0 或更高版本。  
  
2.  在 Web 浏览器的地址栏中，键入报表管理器 URL。 默认情况下，URL 是 http://\<*ComputerName*> / 报表。  
  
### <a name="to-create-a-customized-clickthrough-report"></a>创建自定义的点击链接型报表  
  
1.  导航到要向其中添加自定义点击链接型报表的报表模型。  
  
2.  双击此报表模型。  
  
3.  单击 **“点击链接”**。  
  
4.  选择要向其中附加自定义点击链接型报表的实体。  
  
    > [!NOTE]  
    >  此实体必须与自定义点击链接型报表的基实体相同。  
  
5.  若要在单击选定实体的单个实例时显示此自定义报表，请单击单个实例报表 **“浏览”** 按钮。  
  
     -或-  
  
     若要在单击选定实体的多个实例时显示此自定义报表，请单击多个实例报表 **“浏览”** 按钮。  
  
6.  选择该报表，再单击 **“确定”**。  
  
7.  单击 **“应用”**。  
  
## <a name="see-also"></a>请参阅  
 [点击链接型报表&#40;SSRS&#41;](reports/clickthrough-reports-ssrs.md)  
  
  