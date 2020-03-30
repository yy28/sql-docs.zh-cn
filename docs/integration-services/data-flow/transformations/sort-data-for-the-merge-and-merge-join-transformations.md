---
title: 为合并和合并联接转换排序数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- sort attributes [Integration Services]
- output columns [Integration Services]
ms.assetid: 22ce3f5d-8a88-4423-92c2-60a8f82cd4fd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a73c3aaf23d74857c1c182e4505fb8d602543a8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297786"
---
# <a name="sort-data-for-the-merge-and-merge-join-transformations"></a>为合并转换和合并联接转换排序数据

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]中，合并转换和合并联接转换要求其输入为已排序的数据。 输入数据必须已经过物理排序，且必须对源或上游转换中的输出和输出列设置排序选项。 如果排序选项指示数据是已排序的，而数据实际上不是已排序的，则合并或合并联接操作的结果将是不可预知的。  
  
## <a name="sorting-the-data"></a>对数据进行排序  
 可使用下列方法之一对此数据进行排序：  
  
-   在源中，在用于加载数据的语句中使用 ORDER BY 子句。  
  
-   在数据流中，在合并转换或合并联接转换之前插入一个排序转换。  
  
 如果数据是字符串数据，则合并转换和合并联接转换都需要使用 Windows 排序规则排过序的字符串值。 若要向合并转换和合并联接转换提供使用 Windows 排序规则排过序的字符串值，请使用以下过程。  
  
#### <a name="to-provide-string-values-that-are-sorted-by-using-windows-collation"></a>提供使用 Windows 排序规则排过序的字符串值  
  
-   使用排序转换对数据进行排序。  
  
     排序转换使用 Windows 排序规则对字符串值进行排序。  
  
     -或-  
  
-   首先使用 Transact-SQL CAST 运算符将 **varchar** 值转换为 **nvarchar** 值，然后再使用 Transact-SQL ORDER BY 子句对数据进行排序。  
  
    > [!IMPORTANT]  
    >  由于 ORDER BY 子句使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 排序规则对字符串值进行排序，因此不能单独使用 ORDER BY 子句。 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 排序规则可能产生与 Windows 排序规则不同的排序顺序，这会导致合并转换或合并联接转换生成意外的结果。  
  
## <a name="setting-sort-options-on-the-data"></a>为数据设置排序选项  
 必须为向合并转换和合并联接转换提供数据的源或上游转换设置两个重要的排序属性：  
  
-   输出的 **IsSorted** 属性，指示数据是否已排序。 此属性必须设置为 **True**。  
  
    > [!IMPORTANT]  
    >  将 **IsSorted** 属性的值设置为 **True** 时将不会对数据进行排序。 此属性仅向下游组件提示数据之前已经过排序。  
  
-   输出列的 **SortKeyPosition** 属性，指示单个列是否已排序、其排序顺序以及多个列的排序顺序。 必须为已排序数据的每一列设置此属性。  
  
 如果使用排序转换对数据进行排序，则排序转换将按合并转换或合并联接转换的要求设置这两个属性。 即，排序转换将其输出的 **IsSorted** 属性设置为 **True**，并设置其输出列的 **SortKeyPosition** 属性。  
  
 但是，如果不使用排序转换对数据进行排序，则必须对源或上游转换手动设置这些排序属性。 若要对源或上游转换手动设置这些排序属性，请使用以下过程。  
  
#### <a name="to-manually-set-sort-attributes-on-a-source-or-transformation-component"></a>对源或转换组件手动设置排序属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 **“数据流”** 选项卡中，找到适当的源或上游转换，或将其从 **“工具箱”** 拖到设计图面上。  
  
4.  右键单击组件，并单击“显示高级编辑器”。   
  
5.  单击 **“输入属性和输出属性”** 选项卡。  
  
6.  单击“**组件名称> 输出”\<** ，将“IsSorted”  属性设置为 True  。  
  
    > [!NOTE]  
    >  如果手动将输出的 **IsSorted** 属性设置为 **True** 且没有对数据进行排序，则当你运行该包时，可能会在下游合并或合并联接转换中产生缺失数据或错误数据比较。  
  
7.  展开 **“输出列”** 。  
  
8.  单击要指示为已排序的列，并根据下列准则将其 **SortKeyPosition** 属性设置为非零的整数：  
  
    -   该整数值必须表示一个数值序列，从 1 开始，并按 1 递增。  
  
    -   正整数值表示按升序排序。  
  
    -   负整数值表示按降序排序。 （如果设置为负数，则该数值的绝对值决定该列在排序序列中的位置。）  
  
    -   默认值 0 表示没有对该列进行排序。 请为没有参与排序的输出列保留值 0。  
  
     作为如何设置 **SortKeyPosition** 属性的一个示例，请考虑以下在源中加载数据的 Transact-SQL 语句：  
  
     `SELECT * FROM MyTable ORDER BY ColumnA, ColumnB DESC, ColumnC`  
  
     对于此语句，您可以为每一列按如下所示设置 **SortKeyPosition** 属性：  
  
    -   将 ColumnA 的 **SortKeyPosition** 属性设置为 1。 这表示 ColumnA 是第一个要排序的列，并且是以升序排序。  
  
    -   将 ColumnB 的 **SortKeyPosition** 属性设置为 -2。 这表示 ColumnB 是第二个要排序的列，并且是以降序排序  
  
    -   将 ColumnC 的 **SortKeyPosition** 属性设置为 3。 这表示 ColumnC 是第三个要排序的列，并且是以升序排序。  
  
9. 对每个已排序的列，重复步骤 8。  
  
10. 单击“确定”。   
  
11. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [合并转换](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [合并联接转换](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Integration Services 转换](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路径](../../../integration-services/data-flow/integration-services-paths.md)   
 [数据流任务](../../../integration-services/control-flow/data-flow-task.md)  
  
  
