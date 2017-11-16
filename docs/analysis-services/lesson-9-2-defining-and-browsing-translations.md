---
title: "定义和浏览翻译 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 0e60be99-3768-499c-a22c-a4ec37e61887
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7d55390b1d27fb595b139c06d9dd45b24737522
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-9-2---defining-and-browsing-translations"></a>Lesson 9-2-定义和浏览翻译
翻译是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的名称在特定语言中的表示形式。 对象包括度量值组、度量值、维度、属性、层次结构、KPI、操作和计算成员。 翻译为可支持多种语言的客户端应用程序提供了服务器支持。 通过使用这样的客户端，客户端就可以将区域设置标识符 (LCID) 传递给 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例，该实例则使用 LCID 来确定在为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象提供元数据时要使用哪一组翻译。 如果 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象不包含该语言的翻译或不包含指定对象的翻译，则在将该对象元数据返回给客户端时使用默认语言。 例如，如果一个法国的业务用户从使用法语区域设置的工作站访问多维数据集，则存在法语翻译时，此业务用户将看到法语的成员标题和成员属性值。 但是，如果一个德国的业务用户从使用德语区域设置的工作站上访问同一个多维数据集，则此业务用户将看到德语的成员标题和成员属性值。 有关详细信息，请参阅 [维度翻译](../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)、 [多维数据集翻译](../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)和 [Analysis Services 中的翻译支持](../analysis-services/translation-support-in-analysis-services.md)。  
  
在本主题的任务中，您将为“日期”维度中的一组有限的维度对象和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集中的多维数据集对象定义元数据翻译。 然后浏览这些维度和多维数据集对象，以检查元数据翻译。  
  
## <a name="specifying-translations-for-the-date-dimension-metadata"></a>为“日期”维度元数据指定翻译  
  
1.  打开“日期”维度的维度设计器，然后单击“翻译”选项卡。  
  
    每个维度对象的元数据将以默认语言显示。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集中的默认语言为英语。  
  
2.  在“翻译”选项卡的工具栏上，单击“新建翻译”按钮。  
  
    语言列表将出现在“选择语言”对话框中。  
  
3.  单击“西班牙语(西班牙)”，然后单击“确定”。  
  
    将显示一个新列，在其中您可以将要翻译的元数据对象定义为用西班牙语翻译。 在本教程中，仅翻译了少数对象来举例说明此过程。  
  
4.  在“翻译”选项卡的工具栏上，单击“新建翻译”按钮，在“选择语言”对话框中单击“法语(法国)”，然后单击“确定”。  
  
    将出现另一个语言列，您将在其中定义法语翻译。  
  
5.  在“日期”维度的“标题”对象行中，在“西班牙语(西班牙)”翻译列中键入 **Fecha**，并在“法语(法国)”翻译列中键入 **Temps**。  
  
6.  在“月份名称”属性的“标题”对象行中，在“西班牙语(西班牙)”翻译列中键入 **Mes del Año**，并在“法语(法国)”翻译列中键入 **Mois d'Année**。  
  
    请注意，输入这些翻译时，会出现省略号 (**…**)。 单击此省略号可以指定为属性层次结构的每个成员提供翻译的基础表中的列。  
  
7.  在“月份名称”属性的“西班牙语(西班牙)”翻译中单击省略号 (**…**)。  
  
    “翻译属性数据”对话框将出现。  
  
8.  在“翻译列”列表中，选择“SpanishMonthName”，如下图所示。  
  
    ![数据翻译属性对话框](../analysis-services/media/l9-translations-4.gif "翻译属性数据对话框")  
  
9. 单击“确定”，然后在“月份名称”属性的“法语(法国)”翻译中单击省略号 (**…**)。  
  
10. 在“翻译列”列表中，选择“FrenchMonthName”，然后单击“确定”。  
  
    此过程中的步骤阐释了为维度对象和成员定义元数据翻译的过程。  
  
## <a name="specifying-translations-for-the-analysis-services-tutorial-cube-metadata"></a>为 Analysis Services 教程多维数据集元数据指定翻译  
  
1.  请切换到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器，然后切换到“翻译”选项卡。  
  
    每个多维数据集对象的元数据将以默认语言显示，如下图所示。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集中的默认语言为英语。  
  
    ![默认语言翻译选项卡中的](../analysis-services/media/l9-translations-5.gif "默认翻译选项卡中的语言")  
  
2.  在“翻译”选项卡的工具栏上，单击“新建翻译”按钮。  
  
    语言列表将出现在“选择语言”对话框中。  
  
3.  选择“西班牙语(西班牙)”，然后单击“确定”。  
  
    将显示一个新列，在其中您可以将要翻译的元数据对象定义为用西班牙语翻译。 在本教程中，仅翻译了少数对象来举例说明此过程。  
  
4.  在“翻译”选项卡的工具栏上，单击“新建翻译”按钮，在“选择语言”对话框中选择“法语(法国)”，然后单击“确定”。  
  
    将出现另一个语言列，您将在其中定义法语翻译。  
  
5.  在“日期”维度的“标题”对象行中，在“西班牙语(西班牙)”翻译列中键入 **Fecha**，并在“法语(法国)”翻译列中键入 **Temps**。  
  
6.  在“Internet Sales”度量值组的“标题”对象行中，在“西班牙语(西班牙)”翻译列中键入 **Ventas del lnternet**，并在“法语(法国)”翻译列中键入 **Ventes D'Internet**。  
  
7.  在“Internet Sales-Sales Amount”度量值的“标题”对象行中，在“西班牙语(西班牙)”翻译列中键入 **Cantidad de las Ventas del Internet**，并在“法语(法国)”翻译列中键入 **Quantité de Ventes d'Internet**。  
  
    此过程中的步骤阐释了为多维数据集对象定义元数据翻译的过程。  
  
## <a name="browsing-the-cube-by-using-translations"></a>使用翻译浏览多维数据集  
  
1.  在“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
2.  成功完成部署后，请切换到“浏览器”选项卡，然后单击“重新连接”。  
  
3.  从“数据”窗格中删除所有层次结构和度量值，然后从“透视”列表中选择“[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial”。  
  
4.  在“元数据”窗格中，展开“度量值”，然后展开“Internet Sales”。  
  
    请注意，“Internet Sales-Sales Amount”度量值将以英文形式出现在此度量值组中。  
  
5.  在工具栏上，选择“语言”列表中的“西班牙语(西班牙)”。  
  
    注意，“元数据”窗格中的项将重新填充。 重新填充“元数据”窗格中的项之后，注意“Internet 销售额”度量值将不再出现在“Internet 销售”显示文件夹中。 而是以西班牙语形式出现在名为“Ventas del lnternet”的新显示文件夹中，如下图所示。  
  
    ![Repopulated 元数据窗格](../analysis-services/media/l9-translations-6.gif "Repopulated 元数据窗格")  
  
6.  在“元数据”窗格中，右键单击“Cantidad de las Ventas del Internet”，然后选择“添加到查询”。  
  
7.  在“元数据”窗格中，依次展开“Fecha”和“Fecha.Calendar Date”，右键单击“Fecha.Calendar Date”，然后选择“添加到筛选器”。  
  
8.  在“筛选器”窗格中，选择“CY 2007”作为筛选表达式。  
  
9. 在“元数据”窗格中，右键单击“Mes del Ano”，然后选择“添加到查询”。  
  
    注意，月份名称将以西班牙语显示，如下图所示。  
  
    ![在数据窗格中的月份名称的西班牙语](../analysis-services/media/l9-translations-7.gif "西班牙语在数据窗格中的月份名称")  
  
10. 在工具栏上，选择“语言”列表中的“法语(法国)”。  
  
    注意，月份名称现在将以法语显示，并且度量值名称现在也以法语显示。  
  
## <a name="next-lesson"></a>下一课  
[第 10 课：定义管理角色](../analysis-services/lesson-10-defining-administrative-roles.md)  
  
## <a name="see-also"></a>另请参阅  
[维度翻译](../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)  
[多维数据集翻译](../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)  
[Analysis Services 中的翻译支持](../analysis-services/translation-support-in-analysis-services.md)  
  
  
  

