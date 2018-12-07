---
title: 自定义报表项类库 | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 09ffdde2f04c45d02bfd69369c0fbba8bd2fb5ab
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398880"
---
# <a name="custom-report-item-class-libraries"></a>自定义报表项类库
  自定义报表项使用 Microsoft.ReportDesigner 命名空间中的类。 用于实现自定义报表项的类可分为两个主要类别：旨在支持自定义报表项基础结构的唯一类和用于封装相关报表定义语言 (RDL) 元素功能的托管包装类。 有关如何使用这些类的代码示例，请参阅 [SQL Server Reporting Services Product Samples（SQL Server Reporting Services 产品示例）](https://go.microsoft.com/fwlink/?LinkId=177889)。  
  
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
|CustomProperties|自定义报表项的自定义属性的集合。|  
|高度|自定义报表项控件的高度。|  
|宽度|自定义报表项控件的宽度。|  
|**报告**|报表级别属性（如报表中数据集的列表）的容器。|  
|AltReportItem|备用报表项对象，可在不支持自定义报表项运行时控件时使用。|  
|**样式**|自定义报表项的样式属性。|  
|修饰|用于对控件进行交互式编辑的修饰窗口。|  
|站点|组件的 ISite。|  
|DesignerVerbCollection|控件快捷菜单的自定义谓词的数组。|  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|BeginEdit|激活控件的交互式编辑。|  
|DoDefaultAction|在响应对控件的双击或在控件上按 Return 键时调用。|  
|EndEdit|停用控件的交互式编辑。|  
|GetService|返回一个表示服务的对象。|  
|InitializeNewComponent|当创建新的自定义报表项时调用。|  
|Invalidate|重新绘制控件的整个图面。|  
|OnDragEnter<br /><br /> OnDragDrop|当将对象拖到控件上时调用。|  
|OnPaint|当响应 Paint 事件时调用。|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 这是用于标识自定义报表项的类型的属性。 此名称必须与报表设计器配置文件中 ReportItem 元素的 \<Name> 属性的值相匹配。  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|CustomReportItemAttribute|构造 CustomReportItemAttribute 对象。|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 这是用于指定自定义报表项设计器所使用的显示名称的属性。  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|LocalizedNameAttribute|构造 LocalizedNameAttribute 对象。|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 自定义报表项设计时组件使用修饰类来提供设计图面主矩形之外的区域。 这些区域可用来处理用户界面事件，如鼠标单击和拖放操作。  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|OnShow|当激活修饰时调用。|  
|OnHide|当停用修饰时调用。|  
|Paint|当响应 Paint 事件时调用。|  
|OnDragEnter<br /><br /> OnDragOver<br /><br /> OnDragLeave<br /><br /> OnDragDrop|当将对象拖入修饰时调用。|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 此类用于提供自定义报表项所使用的一组显示服务，以支持自定义报表项设计时组件中的修饰对象。  
  
#### <a name="public-properties"></a>公共属性  
  
|||  
|-|-|  
|AdornerWindowBounds|装饰器窗口的界限。|  
|AdornerWindowRegion|装饰器窗口的区域。|  
|AdornerWindowGraphics|装饰器窗口的图形上下文。|  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|ComponentRectInDesignerFrame|返回转换为设计器框架坐标的组件的边界。|  
|InvalidateAdorner|使装饰器窗口失效。|  
|PointToAdorner|返回转换为装饰器窗口坐标的屏幕坐标中的点。|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 可以从自定义报表项设计时控件使用此类调用表达式编辑器。  
  
#### <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|EditValue|调用以给定的对象值初始化的表达式编辑器。|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 此类是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 字段的集合，用于支持设计环境中的拖放事件。 继承自 IReportItemDataObject。  
  
#### <a name="public-properties"></a>公共属性  
  
|||  
|-|-|  
|DataSetName|包含要拖放的字段的数据集的名称。|  
|**Fields**|要删除的字段 (Microsoft.ReportDesigner.Field) 集合。|  
  
## <a name="see-also"></a>另请参阅  
 [报表定义语言 (SSRS)](../../reporting-services/reports/report-definition-language-ssrs.md)   
 [创建自定义报表项运行时组件](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [创建自定义报表项设计时组件](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
  
  
