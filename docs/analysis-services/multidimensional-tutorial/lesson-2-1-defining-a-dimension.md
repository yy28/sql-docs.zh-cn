---
title: 定义维度 |Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3d0477f9ea54249a52cf50324cc13ae4e9951f2a
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403889"
---
# <a name="lesson-2-1---defining-a-dimension"></a>课程 2-1-定义维度
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

在以下任务中，将使用维度向导生成“日期”维度。  
  
> [!NOTE]  
> 本课要求您已完成课程 1 中的所有课程。  
  
### <a name="to-define-a-dimension"></a>定义维度  
  
1.  在解决方案资源管理器中（在 Microsoft Visual Studio 的右侧），右键单击“维度”文件夹，然后单击“新建维度”。 将显示维度向导。  
  
2.  在“欢迎使用维度向导”页上，单击“下一步”。  
  
3.  在“选择创建方法”页上，确保选中“使用现有表”选项，然后单击“下一步”。  
  
4.  在“指定源信息”页上，确保选中“Adventure Works DW 2012”数据源视图。  
  
5.  在“主表”列表中，选择“日期”。  
  
6.  单击“下一步” 。  
  
7.  在“选择维度属性”页上，选中下列属性旁的复选框：  
  
    -   **日期键**  
  
    -   **完整日期备用键**  
  
    -   **英文月份名称**  
  
    -   **Calendar Quarter**  
  
    -   **Calendar Year**  
  
    -   **Calendar Semester**  
  
8.  将“完整日期备用键”属性的“属性类型”列的设置从“常规”更改为“日期”。 为此，请单击“属性类型”列中的“常规”。 然后单击箭头展开选项。 接下来，单击“日期” > “日历” > “日期”。 单击“确定” 。 重复这些步骤，更改属性的属性类型，具体如下所示：  
  
    -   “英文月份名称”更改为“月份”  
  
    -   “日历季度”更改为“季度”  
  
    -   “日历年”更改为“年”  
  
    -   “日历半期”更改为“半年”  
  
9. 单击“下一步” 。  
  
10. 在“完成向导”页的“预览”窗格中，可以看到“日期”维度及其属性。  
  
11. 单击“完成”以完成向导。  
  
    在解决方案资源管理器的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Tutorial 项目中，“日期”维度将在“维度”文件夹中显示。 在开发环境的中央，维度设计器显示“日期”维度。  
  
12. 在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[定义多维数据集](lesson-2-2-defining-a-cube.md)  
  
## <a name="see-also"></a>请参阅  
[多维模型中的维度](../multidimensional-models/dimensions-in-multidimensional-models.md)  
[使用现有表创建维度](../multidimensional-models/create-a-dimension-by-using-an-existing-table.md)  
[使用维度向导创建维度](../multidimensional-models/create-a-dimension-using-the-dimension-wizard.md)  
  
  
  
