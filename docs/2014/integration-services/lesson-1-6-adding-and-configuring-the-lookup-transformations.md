---
title: 步骤 6：添加并配置查找转换 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c59f723-9707-4407-80ae-f05f483cf65f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f652519efc4b77bd785cdded468fe114f6499200
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62891545"
---
# <a name="step-6-adding-and-configuring-the-lookup-transformations"></a>步骤 6：添加并配置查找转换
  在配置用于从源文件中提取数据的平面文件源后，下一个任务是定义获取 **CurrencyKey** 和 **DateKey** 值所需的查找转换。 查找转换通过将指定输入列中的数据联接到引用数据集中的列来执行查找。 引用数据集可以是现有的表或视图，也可以是新表或 SQL 语句的结果。 在本教程中，查找转换使用 OLE DB 连接管理器连接到包含引用数据集的源数据的数据库。  
  
> [!NOTE]  
>  还可以配置查找转换，以连接到包含引用数据集的缓存。 有关详细信息，请参阅[查找转换](data-flow/transformations/lookup-transformation.md)。  
  
 对于本教程，您将向包中添加以下两个查找转换组件并对其进行配置：  
  
-   一个转换是根据平面文件中匹配的“CurrencyID”**** 列值对“DimCurrency”**** 维度表的“CurrencyKey”**** 列中的值执行查找。  
  
-   一个转换是根据平面文件中匹配的“CurrencyDate”**** 列值对“DimDate”**** 维度表的“DateKey”**** 列中的值执行查找。  
  
 无论在哪种情况下，查找转换都将使用前面创建的 OLE DB 连接管理器。  
  
### <a name="to-add-and-configure-the-lookup-currency-key-transformation"></a>添加并配置 Lookup Currency Key 转换  
  
1.  在 " **SSIS 工具箱**" 中，展开 "**常规**"，然后将 "**查找**" 拖动到 "数据流" 选项卡的设计图**面上。** 将查找直接置于**提取示例货币数据**源下面。  
  
2.  单击“Extract Sample Currency Data”**** 平面文件源，然后将绿色箭头拖到新添加的“查找”**** 转换中，以连接这两个组件。  
  
3.  在“数据流”**** 设计图面上，单击“查找”**** 转换中的“查找”****，然后将该名称更改为 **Lookup Currency Key**。  
  
4.  双击 **Lookup CurrencyKey** 转换，以显示查找转换编辑器。  
  
5.  在“常规”  页上，进行以下选择：  
  
    1.  选择“完全缓存”  。  
  
    2.  在 **“连接类型”** 区域，选择 **“OLE DB 连接管理器”** 。  
  
6.  在“连接”  页上，进行以下选择：  
  
    1.  在“OLE DB 连接管理器”  对话框中，确保显示 **localhost.AdventureWorksDW2012**。  
  
    2.  选择“使用 SQL 查询的结果”****，然后键入或复制以下 SQL 语句：  
  
        ```  
        select * from (select * from [dbo].[DimCurrency]) as refTable  
        where [refTable].[CurrencyAlternateKey] = 'ARS'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'AUD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'BRL'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CAD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CNY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'DEM'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'EUR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'FRF'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'GBP'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'JPY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'MXN'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'SAR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'USD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'VEB'  
        ```  
  
7.  在“列”**** 页上，进行以下选择：  
  
    1.  在“可用输入列”**** 面板中，将“CurrencyID”**** 拖到“可用查找列”**** 面板的“CurrencyAlternateKey”**** 上。  
  
    2.  在“可用查找列”**** 列表中，选中“CurrencyKey”**** 左侧的复选框。  
  
8.  单击“确定”**** 返回“数据流”**** 设计图面。  
  
9. 右键单击“Lookup Currency Key”转换，然后单击“属性”****。  
  
10. 在属性窗口中，验证属性是否`LocaleID`设置为 "**英语（美国）** "，并将 " **DefaultCodePage** " 属性设置为 " **1252**"。  
  
### <a name="to-add-and-configure-the--lookup-datekey-transformation"></a>添加并配置 Lookup DateKey 转换  
  
1.  在“SSIS 工具箱”**** 中，将“查找”**** 拖到“数据流”**** 设计图面上。 将“查找”直接放置在 **Lookup Currency Key** 转换的下面。  
  
2.  单击 **Lookup Currency Key** 转换，并将绿色箭头拖动到新添加的“查找”**** 转换中，以连接这两个组件。  
  
3.  在“选择输入输出”**** 对话框中，单击“输出”**** 列表框中的“查找匹配输出”****，然后单击“确定”****。  
  
4.  在“数据流”**** 设计图面上，在新添加的“查找”**** 转换中单击“查找”****，然后将名称更改为 **Lookup Date Key**。  
  
5.  双击 **Lookup Date Key** 转换。  
  
6.  在“常规”**** 页上，选择“部分缓存”****。  
  
7.  在“连接”**** 页上，进行以下选择：  
  
    1.  在“OLEDB 连接管理器”**** 对话框中，确保已显示 **localhost.AdventureWorksDW2012**。  
  
    2.  在“使用表或视图”**** 框中，键入或选择 **[dbo].[DimDate]**。  
  
8.  在“列”**** 页上，进行以下选择：  
  
    1.  在“可用输入列”**** 面板中，将“CurrencyDate”**** 拖到“可用查找列”**** 面板的“FullDateAlternateKey”**** 上。  
  
    2.  在“可用查找列”**** 列表中，选中“DateKey”**** 左侧的复选框。  
  
9. 在“高级”**** 页上，查看缓存选项。  
  
10. 单击“确定”**** 返回“数据流”**** 设计图面。  
  
11. 双击“Lookup Date Key”转换，然后单击“属性”****。  
  
12. 在属性窗口中，验证属性是否`LocaleID`设置为 "**英语（美国）** "，并将 " **DefaultCodePage** " 属性设置为 " **1252**"。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 7：添加和配置 OLE DB 目标](lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
## <a name="see-also"></a>另请参阅  
 [查找转换](data-flow/transformations/lookup-transformation.md)  
  
  
