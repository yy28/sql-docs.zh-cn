---
title: 配置报表的常规属性（报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], properties
- properties [Reporting Services], general
ms.assetid: 10b941b2-28e6-4408-9ee4-acebc63c8496
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 23184e77efbe41eae3d4de434a30ff8f3a4847ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177027"
---
# <a name="configure-general-properties-for-a-report-report-manager"></a>配置报表的常规属性（报表管理器）
  
### <a name="to-configure-general-report-properties"></a>配置常规报表属性

1.  启动 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)。

2.  在报表管理器中，导航到 "**内容**" 页。 导航到要配置常规属性的报表，并打开该报表。

3.  单击“属性”**** 选项卡。

     或者，如果 "**内容**" 页在详细信息视图中，请单击属性页图标：

     ![属性页图标](media/prop.gif "属性页图标")

4.  将显示 "**常规**属性" 页，您可以按如下所示配置属性：

    -   在 "**属性**" 部分中，可以修改报表名称和说明。

    -   您可以选中 "**在列表视图中隐藏**" 复选框，以便在默认页面布局（列表视图）中打开页面时隐藏项。

    -   在 "**报表定义**" 部分中，单击 "**编辑**" 以提取报表定义的副本。 在本地对报表定义所做的修改不保存在报表服务器上。

         或者，若要从 .rdl 文件中更新报表定义，请单击 "**更新**"。

        > [!NOTE]
        >  如果更新某一报表定义，则必须在更新完成后重置数据源设置。

    -   使用 "**删除**" 或 "**移动**" 按钮删除或移动报表。

    -   还可以创建链接报表。

5.  完成报表的常规属性配置后，单击 "**应用**"。

## <a name="see-also"></a>另请参阅
 [&#40;报表管理器&#41;内容 "页中移动或删除项](report-server/move-or-delete-an-item-report-manager.md) [&#40;报表管理器](../../2014/reporting-services/contents-page-report-manager.md)&#41;&#40;和 SSRS 报表生成器"[常规属性 "页，报表 &#41;&#40;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)报表管理器&#41;[查找、查看和管理报表](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)


