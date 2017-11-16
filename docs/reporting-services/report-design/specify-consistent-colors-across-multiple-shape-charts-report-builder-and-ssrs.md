---
title: "对多个形状图指定一致的颜色（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d52f68e9-2ba7-4bff-9053-4089e5164ab4
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 661d22ed1d594af2c282b61ec28eaaa37bd6821d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs"></a>对多个形状图指定一致的颜色（报表生成器和 SSRS）
  在分页报表的非形状图中， [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 将根据图表中各序列的索引从调色板选择新颜色。 例如，图表中的第一个序列将映射到调色板中的第一个颜色。 但是，对于形状图，该行为则不相同。 在形状图中，调色板中的每个颜色都映射到数据集中的数据点。 例如，数据点 1 映射到调色板中的第一个颜色，数据点 2 映射调色板中的第二个颜色，依此类推。  
  
 如果数据点没有值，该数据点则不显示在形状图中。 这表示显示颜色时将跳过此数据点。 例如，如果点 2 的值为零，点 1 将映射到调色板中的第一个颜色，点 3 将映射到调色板中的第二个颜色。 上述方法非常有用，因为除非在必要情况下，否则当不需要绘制饼图数据集中的空点时，空点不会使用调色板颜色。  
  
 其副作用是，当在报表中显示多个饼图时，饼图可能会对具有相同类别分组的数据点显示不同的颜色。 若要解决该问题，您需要定义映射到类别组而不是各数据值的每一种颜色。 您如何进行定义取决于形状图是否是表或矩阵中的迷你图或者它们是否是报表本身中的形状图。  
  
 图例与序列相连，因此为序列指定的任何颜色将自动在图例上显示。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-consistent-colors-across-multiple-sparkline-shape-charts-in-a-table-or-matrix"></a>在表或矩阵中跨多个迷你图形状图指定一致的颜色  
  
1.  单击图表以显示“图表数据”窗格。  
  
2.  在“类别组”区域中右键单击某一类别，然后单击“类别组属性”。  
  
3.  在“常规”选项卡上的 **“同步其中的组”** 框中，单击要同步其颜色的类别的名称，然后单击 **“确定”**。  
  
## <a name="to-specify-consistent-colors-across-multiple-shape-charts"></a>跨多个形状图指定一致的颜色  
  
1.  右键单击表体外部区域，然后选择“报表属性”。  
  
2.  在 **“代码”**中，将以下代码键入到文本框中。  
  
    ```  
    Private colorPalette As String() = {"Color1", "Color2", "Color3"}  
    Private count As Integer = 0  
    Private mapping As New System.Collections.Hashtable()  
    Public Function GetColor(ByVal groupingValue As String) As String  
        If mapping.ContainsKey(groupingValue) Then  
            Return mapping(groupingValue)  
        End If  
        Dim c As String = colorPalette(count Mod colorPalette.Length)  
        count = count + 1  
        mapping.Add(groupingValue, c)  
        Return c  
    End Function  
    ```  
  
    > [!NOTE]  
    >  您需要用您自己的颜色替换“Color1”。 可以使用命名颜色，例如“Red”，也可以使用表示颜色的六位十六进制值，例如用“#FFFFFF”表示黑色。 如果已定义三种以上的颜色，则需要扩展颜色数组，以使数组中的颜色数与形状图中的点数匹配。 通过指定包含命名颜色或颜色的十六进制表示形式、且以逗号分隔的字符串值列表，可以向数组添加新的颜色。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  右键单击形状图，然后选择“序列属性”。  
  
5.  在“填充”中，单击“表达式”(fx) 按钮可以编辑“颜色”属性的表达式。  
  
6.  键入以下表达式，其中“MyCategoryField”是在 **“类别组”** 区域中显示的字段：  
  
    ```  
    =Code.GetColor(Fields!MyCategoryField)  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [设置图表上序列颜色的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [向图表添加凹凸效果、浮雕和纹理样式（报表生成器和 SSRS）](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [使用调色板定义图表上的颜色（报表生成器和 SSRS）](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [向图表添加空点（报表生成器和 SSRS）](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)   
 [形状图（报表生成器和 SSRS）](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [将多个数据区域链接到同一数据集（报表生成器和 SSRS）](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [嵌套数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [迷你图和数据条（报表生成器和 SSRS）](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
