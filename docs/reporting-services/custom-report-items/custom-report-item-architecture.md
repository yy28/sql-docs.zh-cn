---
title: "自定义报表项体系结构 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, architecture
ms.assetid: 2a88ea46-c9f8-4dd7-aad1-16de11da4f06
caps.latest.revision: 16
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 6ebe0c967ffac1057773dee7d423492371542cee
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="custom-report-item-architecture"></a>自定义报表项体系结构
  自定义报表项是对报表定义语言 (RDL) 的扩展，允许开发人员添加在 RDL 中并不固有支持的功能或扩展现有控件的功能。 有两个用于自定义报表项的主要组件：运行时组件和设计时组件。 这些组件作为 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 程序集实现，并且可用任何符合 CLS 的语言编写。  
  
## <a name="the-run-time-component"></a>运行时组件  
 自定义报表项的运行时组件由报表处理器在运行时调用。 该运行时组件接受报表处理器在运行时传递的数据、处理这些数据并返回包含呈现的自定义报表项的图像。  
  
 ![自定义报表项运行时组件](../../reporting-services/custom-report-items/media/customreportitemrun-timecomponentarchitecture.gif "自定义报表项运行时组件")  
  
## <a name="the-design-time-component"></a>设计时组件  
 设计时组件允许在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 的报表设计器界面中定义和操作自定义报表项。 设计时组件由若干子控件构成，这些子控件控制设计环境中自定义报表项的外观和属性。  
  
 ![自定义报表项设计时组件](../../reporting-services/custom-report-items/media/customreportitemdesign-timecomponentarchitecture.gif "自定义报表项设计时组件")  
  
## <a name="see-also"></a>另请参阅  
 [创建自定义报表项运行时组件](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [创建自定义报表项设计时组件](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [如何︰ 部署自定义报表项](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
