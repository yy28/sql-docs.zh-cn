---
title: "开发的自定义 ForEach 枚举器的用户界面 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e743464fcf482ea51f0cde78d692b367c2be525b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>为自定义 ForEach 枚举器开发用户界面
  重写基类的属性和方法的实现以提供自定义功能后，您可能需要为 Foreach 枚举器创建自定义用户界面。 如果未创建自定义用户界面，用户只能使用“属性”窗口来配置新的自定义 Foreach 枚举器。  
  
 在自定义用户界面项目或程序集中，可以创建一个实现 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI> 的类。 此类派生自 System.Windows.Forms.UserControl，通常用于创建托管其他 Windows 窗体控件的复合控件。 你创建的控件显示在**枚举器配置**区域**集合**选项卡**Foreach 循环编辑器**。  
  
> [!IMPORTANT]  
>  签名以及构建自定义用户界面和中所述在全局程序集缓存中安装后[生成、 部署和调试自定义对象](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)，请记得提供中此类的完全限定的名称<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A>属性<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>。  
  
## <a name="coding-the-user-interface-control-class"></a>编写用户界面控件类代码  
  
### <a name="initializing-the-user-interface"></a>初始化用户界面  
 可以重写 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A> 方法以缓存对主机对象以及包中定义的连接管理器集合和变量集合的引用。  
  
### <a name="setting-properties-on-the-user-interface-control"></a>设置用户界面控件的属性  
 UserControl 类，从其用户界面类派生，旨在用作复合控件，承载其他 Windows 窗体控件中。 由于此类承载其他控件，因此您可以像在任何 Windows 窗体应用程序中一样，通过拖放控件、排列控件、设置控件属性以及在运行时响应控件的事件来设计您自己的自定义用户界面。  
  
### <a name="saving-settings"></a>保存设置  
 可以重写 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A> 方法，以在用户关闭编辑器时，将用户选择的值从控件复制到枚举器的属性。  
  
## <a name="see-also"></a>另请参阅  
 [创建自定义 Foreach 枚举器](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)   
 [编码的自定义 Foreach 枚举器](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
  
  

