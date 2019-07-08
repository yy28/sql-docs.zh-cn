---
title: 创建链接报表 | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6dad85f35be1d7fb26f4c9eef6241e01baadb692
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492816"
---
# <a name="create-a-linked-report"></a>创建链接报表
  链接报表是提供对现有报表的访问点的报表服务器项。 从概念上说，它与用于运行程序或打开文件的程序快捷方式类似。  
  
 链接报表是从现有报表派生的，保留原始报表的报表定义。 链接报表始终会继承原始报表的报表布局和数据源属性。 所有其他属性和设置都可以与原始报表不同，其中包括安全性、参数、位置、订阅和计划。  
  
 如果希望创建现有报表的其他版本，则可以创建链接报表。 例如，可以使用一个区域销售额报表来为所有销售区域创建区域特定的报表。  
  
 虽然链接报表通常基于参数化报表，但并不一定需要使用参数化报表。 每当您想使用不同的设置部署现有报表时，都可以创建链接报表。  
  
## <a name="to-create-a-linked-report"></a>创建链接报表  
  
1. 在 web 门户中，导航到所需的报表，右键单击它并选择**管理**从下拉列表菜单。

2. 上**管理<reportname>** 页上，选择**创建链接的报表**。  
  
3. 输入新链接报表的名称。 输入可选说明。  
  
4. 若要选择不同的报表的文件夹，选择右侧的省略号按钮 （...）***位置***。  导航到新文件夹的报表并选择**选择**。 如果不选择其他文件夹，在当前文件夹中创建链接的报表。  
  
5. 选择“创建”  。 创建链接的报表。  

6. 下**高级**，选择不同**报表超时**如果需要，则值为，然后选择**应用**以保存所做的更改。
  
     链接报表的图标与报表服务器管理的其他项不同。 下面的图标表示链接报表：  
  
     ![链接报表图标](../../reporting-services/report-server/media/hlp-16linked.gif "链接报表图标")  
  
## <a name="see-also"></a>另请参阅  

 [Reporting Services 概念 &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)  
 [报表服务器的 Web 门户（SSRS 本机模式）](../../reporting-services/web-portal-ssrs-native-mode.md)
  
