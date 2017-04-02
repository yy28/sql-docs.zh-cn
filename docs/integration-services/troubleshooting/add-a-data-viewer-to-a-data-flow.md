---
title: "将数据查看器添加到数据流 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "数据查看器 [Integration Services]"
  - "数据流 [Integration Services], 数据查看器"
  - "添加数据查看器"
ms.assetid: 5e573274-a170-4132-bfc8-a8ff3a8411e4
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# 将数据查看器添加到数据流
  本主题介绍如何在数据流中添加和配置数据查看器。 数据查看器可以显示在两个数据流组件之间移动的数据。 例如，数据查看器可以显示在数据流中的转换修改数据之前从数据源中提取的数据。  
  
 路径将一个数据流组件的输出连接到另一个组件的输入，以此连接数据流中的组件。  
  
 在可以将数据查看器添加到包之前，包必须包括一个数据流任务和至少两个已连接在一起的数据流组件。  
  
 将数据查看器添加到错误输出即可查看对错误的描述以及发生了错误的列的名称。 默认情况下，错误输出只包括针对错误和列的数字标识符。  
  
### 将数据查看器添加到数据流  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  如果 **“控制流”** 选项卡尚未处于活动状态，请单击该选项卡。  
  
4.  单击要将数据查看器附加到其数据流的数据流任务，然后单击 **“数据流”** 选项卡。  
  
5.  右键单击两个数据流组件之间的路径，然后单击“编辑”。  
  
6.  在 **“常规”** 页上，可以查看和编辑路径属性。 例如，从“路径批注”下拉列表中，你可以选择要在路径旁边显示的批注。  
  
7.  在 **“元数据”** 页上，您可以查看列元数据并将元数据复制到剪贴板。  
  
8.  在 **“数据查看器”** 页上，单击 **“启用数据查看器”**。  
  
9. 在“要显示的列”区域中，选择要在数据查看器中显示的列。 默认情况下，所有可用列都处于选定状态并在 **“已显示的列”** 列表中列出。 选择不希望使用的列，然后单击向左键，将它们移到 **“未使用的列”** 列表中。  
  
    > [!NOTE]  
    >  在网格中，表示 DT_DATE、DT_DBTIME2、DT_FILETIME、DT_DBTIMESTAMP、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 数据类型的值显示为 ISO 8601 格式字符串，空间分隔符将替代 **T** 分隔符。 表示 DT_DATE 和 DT_FILETIME 数据类型的值包括七位秒小数。 因为 DT_FILETIME 数据类型仅存储三位秒小数，网格会将其余四位显示为零。 表示 DT_DBTIMESTAMP 数据类型的值包含三位秒小数。 对于表示 DT_DBTIME2、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 数据类型的值，秒小数的数字位数与为列数据类型指定的小数位数对应。 有关 ISO 8601 格式的详细信息，请参阅 [Date and Time Formats](../Topic/Date%20and%20Time%20Formats.md)。 有关数据类型的详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
10. 单击 **“确定”**。  
  
## 另请参阅  
 [Integration Services 转换](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路径](../../integration-services/data-flow/integration-services-paths.md)   
 [数据流](../../integration-services/data-flow/data-flow.md)   
 [调试数据流](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
  