---
title: "自定义报表项类库 |Microsoft 文档"
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
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
caps.latest.revision: 27
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f216228c01e835e88cd9d4c7d7d4190648a386db
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="custom-report-item-class-libraries"></a>自定义报表项类库
  自定义报表项使用的类**Microsoft.ReportDesigner**命名空间。 用于实现自定义报表项的类可分为两个主要类别：旨在支持自定义报表项基础结构的唯一类和用于封装相关报表定义语言 (RDL) 元素功能的托管包装类。 有关如何使用这些类的代码示例，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="custom-report-item-infrastructure-classes"></a>自定义报表项基础结构类  
 以下类用于实现自定义报表项。  
  
> [!NOTE]  
>  以下表并非完整列表；这些表仅包括每个类最常用的属性和方法。  
  
### <a name="microsoftreportdesignercustomreportitemdesigner"></a>Microsoft.ReportDesigner.CustomReportItemDesigner  
 这是自定义报表项主类。 自定义报表项实现的主类必须继承自此类。  
  
#### <a name="public-properties"></a>公共属性  
  
|||  
|-|-|  
|**名称**|自定义报表项的名称。|  
|**类型**|自定义报表项的类型。|  
|**CustomData**|用于封装在设计时指定的自定义报表项数据属性的 <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 对象。|  
|**自定义属性**|自定义报表项的自定义属性的集合。|  
|**高度**|自定义报表项控件的高度。|  
|**宽度**|自定义报表项控件的宽度。|  
|**报告**|报表级别属性（如报表中数据集的列表）的容器。|  
|**AltReportItem**|备用报表项对象，可在不支持自定义报表项运行时控件时使用。|  
|**样式**|自定义报表项的样式属性。|  
|**修饰**|用于对控件进行交互式编辑的修饰窗口。|  
|**站点**|**ISite**的组件。|  
|**DesignerVerbCollection**|控件快捷菜单的自定义谓词的数组。|  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|**BeginEdit**|激活控件的交互式编辑。|  
|**DoDefaultAction**|在响应对控件的双击或在控件上按 Return 键时调用。|  
|**EndEdit**|停用控件的交互式编辑。|  
|**GetService**|返回一个表示服务的对象。|  
|**InitializeNewComponent**|当创建新的自定义报表项时调用。|  
|**使无效**|重新绘制控件的整个图面。|  
|**OnDragEnter**<br /><br /> **OnDragDrop**|当将对象拖到控件上时调用。|  
|**OnPaint**|调用以响应**绘制**事件。|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 这是用于标识自定义报表项的类型的属性。 该名称必须匹配的值\<**名称**> 特性**ReportItem**报表设计器配置文件中的元素。  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|**CustomReportItemAttribute**|构造 CustomReportItemAttribute 对象。|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 这是用于指定自定义报表项设计器所使用的显示名称的属性。  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|**LocalizedNameAttribute**|构造 LocalizedNameAttribute 对象。|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 **修饰**类由自定义报表项设计时组件用于提供在设计图面的主矩形之外的区域。 这些区域可用来处理用户界面事件，如鼠标单击和拖放操作。  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|**OnShow**|时调用**修饰**激活。|  
|**OnHide**|时调用**修饰**停用。|  
|**绘制**|调用以响应**绘制**事件。|  
|**OnDragEnter**<br /><br /> **OnDragOver**<br /><br /> **OnDragLeave**<br /><br /> **OnDragDrop**|当将对象拖入时调用**修饰**。|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 此类用于提供的自定义报表项用于支持显示服务的集合**修饰**自定义报表项设计时组件的对象。  
  
#### <a name="public-properties"></a>公共属性  
  
|||  
|-|-|  
|**AdornerWindowBounds**|装饰器窗口的界限。|  
|**AdornerWindowRegion**|装饰器窗口的区域。|  
|**AdornerWindowGraphics**|装饰器窗口的图形上下文。|  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|**ComponentRectInDesignerFrame**|返回转换为设计器框架坐标的组件的边界。|  
|**InvalidateAdorner**|使装饰器窗口失效。|  
|**PointToAdorner**|返回转换为装饰器窗口坐标的屏幕坐标中的点。|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 可以从自定义报表项设计时控件使用此类调用表达式编辑器。  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|**EditValue**|调用以给定的对象值初始化的表达式编辑器。|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 此类是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 字段的集合，用于支持设计环境中的拖放事件。 继承自**IReportItemDataObject**。  
  
#### <a name="public-properties"></a>公共属性  
  
|||  
|-|-|  
|**数据集名称**|包含要拖放的字段的数据集的名称。|  
|**字段**|字段的集合 (**Microsoft.ReportDesigner.Field**) 被删除。|  
  
## <a name="see-also"></a>另请参阅  
 [报表定义语言 &#40;SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)   
 [创建自定义报表项运行时组件](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [创建自定义报表项设计时组件](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
  
  
