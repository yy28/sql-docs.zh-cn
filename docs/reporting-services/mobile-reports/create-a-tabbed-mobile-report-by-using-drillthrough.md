---
title: "通过使用钻取创建选项卡式移动报表 |Reporting Services 移动报表 |Microsoft 文档"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6554f808c19540d2a3b7cbe3fdf4e86c5fe7a357
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>通过使用钻取创建选项卡式移动报表
了解如何使用钻取功能和参数创建外观和行为与选项卡式报表类似的 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 移动报表。

例如，在此报表中，顶部仪表的行为与选项卡类似。 单击“运输”仪表时，图表其余部分中的数据将筛选为运输数据。

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

在后台，这实际上是五个单独报表的集合，每个报表都具有不同的参数，用于筛选报表以匹配在报表顶部所选的仪表。 首先，创建所有五个报告，然后对于每个五个报告，你向其他四个仪表 drillthroughs 到其他四个报告。

以下是此示例的步骤。

## <a name="create-the-basic-report"></a>创建基本报表

1. 使用五个仪表创建名为 Sales 的报表：

    * Sales
    * 运输
    * 燃料
    * 存储器
    * 杂项费用

   ![01-销售-移动的报表的发布，服务器](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. 设置**重音**到**上**为销售仪表中，因此它将与之相反的其余部分报告 — 在这种情况下，黑色上为白色。

    ![01a-Sales-Accent-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. 将其保存到[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]报表服务器。

## <a name="make-copies-of-the-report"></a>创建报表的副本

1. 创建的销售报表的四个副本，并将它们命名： 

    * 运输
    * 燃料
    * 存储器
    * 杂项费用

3. 保存到[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]报表服务器。

## <a name="set-the-gauge-as-a-drillthrough"></a>设置仪表作为钻取

在本部分中，你作为钻取到其各自的报告设置 （而不是销售仪表中） 的每个仪表。

1. 在销售报表中，选择运输仪表。

    ![02-Sales-Create-DrillThrough-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. 与**布局**的选项卡，在**Visual 属性**窗格中选择**钻取目标**。

3. 选择**移动报表**。

4. 导航到并选择在这种情况下，将为钻取操作-目标的报表"财务-运输。"

    ![03-Sales-Select-Dashboard-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. 在**配置目标报表**，选择参数以筛选报表，并选择**应用**。

   ![04-Sales-Apply-Parameters-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. 为每个销售报表中的其他仪表重复这些步骤。 

## <a name="set-the-gauges-for-the-other-reports"></a>设置其他报表的仪表

1.  打开运输报表，根据钻取到销售报表，而其他三个仪表作为 drillthroughs 到其相应的报表设置销售仪表。

2. 仍在运输报表中，设置**重音**到运输仪表**上**，与之相反的报表的其余部分。

3. 对燃料、 存储和杂项费用报表重复这些步骤。 

## <a name="view-the-report-in-the-web-portal"></a>在 web 门户中查看报表

1. 转到[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]报表服务器并打开一个报表。 

2. 请注意每个仪表右上角有一个钻取图标。

    ![Web-Viewer-drillthrough-icon-mobile-report-builder](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. 选择一个仪表转到报表筛选到该仪表的数据。

   ![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>另请参阅
    
* [将参数添加到移动报表](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [添加从某个移动报表到其他移动报表或 URL 的钻取](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  


