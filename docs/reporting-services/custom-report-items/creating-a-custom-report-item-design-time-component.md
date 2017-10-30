---
title: "创建一个自定义报表项设计时组件，|Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- custom report items, creating
ms.assetid: 323fd58a-a462-4c48-b188-77ebc0b4212e
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0b1f5649db2f99957ad3b2452b02d2f7b2db01cb
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="creating-a-custom-report-item-design-time-component"></a>创建自定义报表项设计时组件
  自定义报表项设计时组件是一种可在 Visual Studio 报表设计器环境中使用的控件。 自定义报表项设计时组件可提供能接受拖放操作的激活的设计图面，可与 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 属性浏览器集成，且可提供自定义属性编辑器。  
  
 通过自定义报表项设计时组件，用户可以在设计环境下在报表中放置自定义报表项，可以针对自定义报表项设置自定义数据属性，然后可以将自定义报表项另存为报表项目的一部分。  
  
 在开发环境中使用设计时组件设置的属性可通过宿主设计环境序列化和反序列化，然后存储为报表定义语言 (RDL) 文件中的元素。 报表由报表处理器执行时，使用设计时组件设置的属性将由报表处理器传递给自定义报表项运行时组件，后者将呈现自定义报表项，并将自定义报表项传递回报表处理器。  
  
> [!NOTE]  
>  作为实现自定义报表项设计时组件[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]组件。 本文档将介绍自定义报表项设计时组件所特有的实现细节。 有关开发组件使用的详细信息[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，请参阅[Visual Studio 中的组件](http://go.microsoft.com/fwlink/?LinkId=116576)MSDN 库中。  
  
 完全实现的自定义报表项的示例，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="implementing-a-design-time-component"></a>实现设计时组件  
 自定义报表项设计时组件的主类继承自**Microsoft.ReportDesigner.CustomReportItemDesigner**类。 除了标准的属性用于[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]组件类应定义控制， **CustomReportItem**属性。 此属性必须与如在 reportserver.config 文件中定义的相应自定义报表项的名称对应。 有关 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 属性的列表，请参阅 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档中的“属性”。  
  
 以下代码示例显示的是将应用到自定义报表项设计时控件的属性：  
  
```csharp  
namespace PolygonsCRI  
{  
    [LocalizedName("Polygons")]  
    [Editor(typeof(CustomEditor), typeof(ComponentEditor))]  
        [ToolboxBitmap(typeof(PolygonsDesigner),"Polygons.ico")]  
        [CustomReportItem("Polygons")]  
  
    public class PolygonsDesigner : CustomReportItemDesigner  
    {  
...  
```  
  
### <a name="initializing-the-component"></a>初始化组件  
 可以使用 <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 类传递自定义报表项的用户指定属性。 实现**CustomReportItemDesigner**类应重写**InitializeNewComponent**方法来创建你的组件的新实例<xref:Microsoft.ReportingServices.RdlObjectModel.CustomData>类并将其设置为默认值。  
  
 下面的代码示例显示的自定义报表项设计时组件类重写示例**CustomReportItemDesigner.InitializeNewComponent**方法以初始化组件的<xref:Microsoft.ReportingServices.RdlObjectModel.CustomData>类：  
  
```csharp  
public override void InitializeNewComponent()  
        {  
            CustomData = new CustomData();  
            CustomData.DataRowHierarchy = new DataHierarchy();  
  
            // Shape grouping  
            CustomData.DataRowHierarchy.DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].Group.Name = Name + "_Shape";  
            CustomData.DataRowHierarchy.DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Point grouping  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.Name = Name + "_Point";  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Static column  
            CustomData.DataColumnHierarchy = new DataHierarchy();  
            CustomData.DataColumnHierarchy.DataMembers.Add(new DataMember());  
  
            // Points  
            IList<IList<DataValue>> dataValues = new List<IList<DataValue>>();  
            CustomData.DataRows.Add(dataValues);  
            CustomData.DataRows[0].Add(new List<DataValue>());  
            CustomData.DataRows[0][0].Add(NewDataValue("X", ""));  
            CustomData.DataRows[0][0].Add(NewDataValue("Y", ""));  
        }  
```  
  
### <a name="modifying-component-properties"></a>修改组件属性  
 你可以修改**CustomData**以下几种方式设计环境中的属性。 可以使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 属性浏览器修改任何由设计时组件公开且以 <xref:System.ComponentModel.BrowsableAttribute> 属性标记的特性。 此外，你可以修改属性，通过将项拖到自定义报表项的设计图面上或通过右键单击设计环境中的控件并选择**属性**上以显示一个自定义属性窗口的快捷菜单。  
  
 下面的代码示例演示**Microsoft.ReportDesigner.CustomReportItemDesigner.CustomData**属性具有<xref:System.ComponentModel.BrowsableAttribute>应用属性：  
  
```csharp  
[Browsable(true), Category("Data")]  
public string DataSetName  
{  
      get  
      {  
         return CustomData.DataSetName;  
      }  
      set  
      {  
         CustomData.DataSetName = value;  
      }  
   }  
  
```  
  
 可以为您的设计时组件提供自定义属性编辑器对话框。 自定义属性编辑器实现应继承自 <xref:System.ComponentModel.ComponentEditor> 类，并应创建可用于属性编辑的对话框实例。  
  
 下面的示例显示了继承自 <xref:System.ComponentModel.ComponentEditor> 的类的实现，并显示了自定义属性编辑对话框：  
  
```csharp  
internal sealed class CustomEditor : ComponentEditor  
{  
   public override bool EditComponent(  
      ITypeDescriptorContext context, object component)  
    {  
     PolygonsDesigner designer = (PolygonsDesigner)component;  
     PolygonProperties dialog = new PolygonProperties();  
     dialog.m_designerComponent = designer;  
     DialogResult result = dialog.ShowDialog();  
     if (result == DialogResult.OK)  
     {  
        designer.Invalidate();  
        designer.ChangeService().OnComponentChanged(designer, null, null, null);  
        return true;  
     }  
     else  
        return false;  
    }  
}  
```  
  
 自定义属性编辑器对话框可以调用报表设计器表达式编辑器。 在下面的示例中，在用户选择相应组合框中的第一个元素时，会调用表达式编辑器：  
  
```csharp  
private void EditableCombo_SelectedIndexChanged(object sender,   
    EventArgs e)  
{  
   ComboBox combo = (ComboBox)sender;  
   if (combo.SelectedIndex == 0 && m_launchEditor)  
   {  
      m_launchEditor = false;  
      ExpressionEditor editor = new ExpressionEditor();  
      string newValue;  
      newValue = (string)editor.EditValue(null, m_designerComponent.Site, m_oldComboValue);  
      combo.Items[0] = newValue;  
   }  
}  
  
```  
  
### <a name="using-designer-verbs"></a>使用设计器谓词  
 设计器谓词是与事件处理程序链接的菜单命令。 在设计环境下使用自定义报表项运行时控件时，可以添加将显示在相应组件的快捷菜单中的设计器谓词。 可以通过从运行时组件中返回的可用设计器谓词的列表**谓词**属性。  
  
 下面的代码示例显示的是将添加到 <xref:System.ComponentModel.Design.DesignerVerbCollection> 的设计器谓词和事件处理程序，以及事件处理程序代码：  
  
```csharp  
public override DesignerVerbCollection Verbs  
{  
    get  
    {  
        if (m_verbs == null)  
        {  
            m_verbs = new DesignerVerbCollection();  
            m_verbs.Add(new DesignerVerb("Proportional Scaling", new EventHandler(OnProportionalScaling)));  
         m_verbs[0].Checked = (GetCustomProperty("poly:Proportional") == bool.TrueString);  
        }  
  
        return m_verbs;  
    }  
}  
  
private void OnProportionalScaling(object sender, EventArgs e)  
{  
   bool proportional = !  
        (GetCustomProperty("poly:Proportional") == bool.TrueString);  
   m_verbs[0].Checked = proportional;  
   SetCustomProperty("poly:Proportional", proportional.ToString());  
   ChangeService().OnComponentChanged(this, null, null, null);  
   Invalidate();  
}  
```  
  
### <a name="using-adornments"></a>使用修饰  
 此外可以实现自定义报表项类**Microsoft.ReportDesigner.Design.Adornment**类。 使用修饰后，自定义报表项控件可提供设计图面主矩形之外的区域。 这些区域可用来处理用户界面事件，如鼠标单击和拖放操作。 **修饰**中定义的类[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **Microsoft.ReportDesigner**命名空间是一种传递实现的<xref:System.Windows.Forms.Design.Behavior.Adorner>类在 Windows 窗体中找到。 有关完整文档**装饰器**类，请参阅[行为服务概述](http://go.microsoft.com/fwlink/?LinkId=116673)MSDN 库中。 有关示例代码，实现**Microsoft.ReportDesigner.Design.Adornment**类，请参阅[SQL Server Reporting Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
 有关在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中如何对 Windows 窗体进行编程和使用 Windows 窗体的详细信息，请参见 MSDN Library 中的以下主题：  
  
-   Design-Time Attributes for Components（组件的设计时属性）  
  
-   中的组件[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]  
  
-   Walkthrough: Creating a Windows Forms Control that Takes Advantage of Visual Studio Design-Time Features（演练：创建一个利用 Visual Studio 设计时功能的 Windows 窗体控件）  
  
## <a name="see-also"></a>另请参阅  
 [自定义报表项体系结构](../../reporting-services/custom-report-items/custom-report-item-architecture.md)   
 [创建自定义报表项运行时组件](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [自定义报表项类库](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)   
 [如何︰ 部署自定义报表项](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  

