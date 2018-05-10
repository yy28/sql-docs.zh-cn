---
title: 步骤 2：添加和配置平面文件连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 9a77dd32-d8c2-4961-ad37-2a971f9d6043
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0a114b291767449f4e187c0d3747dac7a77435b8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-2---adding-and-configuring-a-flat-file-connection-manager"></a>第 1-2 课 — 添加和配置平面文件连接管理器
在本任务中，将在刚创建的包中添加一个平面文件连接管理器。 通过平面文件连接管理器，包可从平面文件中提取数据。 使用平面文件连接管理器，可以指定包从平面文件中提取数据时要应用的文件的名称与位置、区域设置与代码页以及文件格式，其中包括列分隔符。 另外，还可以为各个列手动指定数据类型；也可以使用“提供列类型建议”对话框，自动将提取出来的数据列映射到 **数据类型。**[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]  
  
必须为要使用的每种文件格式创建一个新的平面文件连接管理器。 因为本教程从多个数据格式完全相同的平面文件提取数据，所以只需为您的包添加和配置一个平面文件连接管理器。  
  
在本教程中，将在平面文件连接管理器中配置以下属性：  
  
-   **列名：** 因为平面文件没有列名，因此平面文件连接管理器将创建默认的列名。 这些默认名称不能用于标识每个列代表的内容。 若要使这些默认名称更有用，需要将默认名称改为要加载平面文件数据的事实数据表匹配的名称。  
  
-   **数据映射：**为平面文件连接管理器指定的数据类型映射，将由所有引用该连接管理器的平面文件数据源组件使用。 可以使用平面文件连接管理器，或者使用“提供列类型建议”对话框来手动映射数据类型。 在本教程中，将查看“提供列类型建议”对话框中建议的映射，然后在“平面文件连接管理器编辑器”对话框中手动设置必要的映射。  
  
平面文件连接管理器提供了有关数据文件的区域设置信息。 如果未将计算机配置为使用区域设置选项“英语(美国)”，则必须在“平面文件连接管理器编辑器”对话框中设置其他属性。   
  
### <a name="to-add-a-flat-file-connection-manager-to-the-ssis-package"></a>向 SSIS 包添加平面文件连接管理器  
  
1.  右键单击“连接管理器”区域中的任意位置，再单击“新建平面文件连接”。  
  
2.  在“平面文件连接管理器编辑器”对话框的“连接管理器名称”字段中，键入“Sample Flat File Source Data”。  
  
3.  单击 **“浏览”**。  
  
4.  在“打开”对话框中，找到计算机上的 SampleCurrencyData.txt 文件。   
  
    示例数据与 [!INCLUDE[ssIS](../includes/ssis-md.md)] 课程包一起提供。 要下载示例数据和课程包，请执行以下操作：  
  
    1.  导航到 [Integration Services 产品示例](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  单击 **“下载”** 选项卡。  
  
    3.  单击 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 文件。  
  
5.  清除第一个数据行复选框中的“列名”。  
  
### <a name="to-set-locale-sensitive-properties"></a>设置受区域设置影响的属性  
  
1.  在“平面文件连接管理器编辑器”对话框中，单击“常规”。  
  
2.  将“区域设置”设置为“英语(美国)”，并将“代码页”设置为 1252。  
  
### <a name="to-rename-columns-in-the-flat-file-connection-manager"></a>重命名平面文件连接管理器中的列  
  
1.  在“平面文件连接管理器编辑器”对话框中，单击“高级”。  
  
2.  在属性窗格中，进行如下更改：  
  
    -   将 **Column 0** 名称属性改为 **AverageRate**。  
  
    -   将 **Column 1** 名称属性改为 **CurrencyID**。  
  
    -   将 **Column 2** 名称属性改为 **CurrencyDate**。  
  
    -   将 **Column 3** 名称属性改为 **EndOfDayRate**。  
  
    > [!NOTE]  
    > 默认情况下，所有四个列最初都设置为字符串数据类型 [DT_STR]，其 **OutputColumnWidth** 为 50。  
  
### <a name="to-remap-column-data-types"></a>重新映射列数据类型  
  
1.  在“平面文件连接管理器编辑器”对话框中，单击“建议类型”。  
  
    [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 根据前 200 行数据自动建议最合适的数据类型。 您还可以将这些建议选项改为增加或减少取样数据，以便指定整数数据或布尔数据的默认数据类型，或添加作为填充量添加到字符串列中的空格。  
  
    现在，不对“提供列类型建议”对话框中的选项进行任何更改，单击“确定”使 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供列数据类型的建议。 这样，将转到“平面文件连接管理器编辑器”对话框的“高级”窗格，在此可以查看 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 建议使用的列数据类型。 （如果单击“取消”，则不对列元数据提供任何建议，并使用默认字符串 (DT_STR) 数据类型。）  
  
    在本教程中， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 为 SampleCurrencyData.txt 文件中的数据建议了下表第二列中显示的数据类型。 但是，目标中的列要求的数据类型（将在以后的步骤中定义）显示在下表的最后一列。  
  
    |平面文件列|建议的类型|目标列|目标类型|  
    |--------------------|------------------|----------------------|--------------------|  
    |AverageRate|float [DT_R4]|FactCurrency.AverageRate|FLOAT|  
    |CurrencyID|string [DT_STR]|DimCurrency.CurrencyAlternateKey|nchar(3)|  
    |CurrencyDate|date [DT_DATE]|DimDate.FullDateAlternateKey|日期|  
    |EndOfDayRate|float [DT_R4]|FactCurrency.EndOfDayRate|FLOAT|  
  
    为 **CurrencyID** 列建议的数据类型与目标表中字段的数据类型不兼容。 由于 `DimCurrency.CurrencyAlternateKey` 的数据类型为 nchar (3)， **CurrencyID** 必须从字符串 [DT_STR] 改为字符串 [DT_WSTR]。 另外，字段 `DimDate.FullDateAlternateKey` 被定义为日期数据类型，因此 **CurrencyDate** 需要从日期 [DT_Date] 改为数据库日期 [DT_DBDATE]。  
  
2.  在列表中选择“CurrencyID”列，在属性窗格中将列 **CurrencyID** 的数据类型从字符串 [DT_STR] 改为 Unicode 字符串 [DT_WSTR]。  
  
3.  在属性窗格中，将列 **CurrencyDate** 的数据类型从日期 [DT_DATE] 改为数据库日期 [DT_DBDATE]。  
  
4.  单击“确定” 。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[步骤 3：添加并配置 OLE DB 连接管理器](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
## <a name="see-also"></a>另请参阅  
[平面文件连接管理器](../integration-services/connection-manager/flat-file-connection-manager.md)  
[Integration Services 数据类型](../integration-services/data-flow/integration-services-data-types.md)  
  
  
  
