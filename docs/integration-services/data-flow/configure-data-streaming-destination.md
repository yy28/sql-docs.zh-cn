---
title: "配置数据流目标 | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1"
ms.assetid: bcdbb833-20c8-47ff-a641-bb517f9a1af3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# 配置数据流目标
  通过使用“数据流目标高级编辑器”  对话框配置数据流目标。 在数据流设计器中双击该组件或右键单击该组件然后单击“编辑”来打开此对话框。  
  
 此对话框包含三个选项卡：“组件属性” 、“输入列” 和“输入属性和输出属性” 。  
  
## “组件属性”选项卡  
 该选项卡具有以下可编辑字段：  
  
|字段|Description|  
|-----------|-----------------|  
|名称|包中数据流目标组件的名称。|  
|ValidateExternalMetadata|指示设计时是否使用外部数据源对组件进行了验证。 如果设置为 False，对外部数据源的验证将推迟到运行时。|  
|IDColumnName|数据馈送发布向导生成的视图有此附加 ID 列。 当其他应用程序将该数据用作 OData 馈送时，ID 列将作为数据流的输出数据的 EntityKey。<br /><br /> 此列的默认值为 _ID。 可以为 ID 列指定不同名称。|  
  
## “输入列”选项卡  
 在此选项卡的顶部窗格中，你会看到所有可用输入列。 选择你想要在此组件的输出中包含的列。 所选的列会显示在底部窗格的列表中。 可以通过在列表中 **输出别名** 字段中输入新名称来更改输出列名。  
  
## “输入属性和输出属性”选项卡  
 类似于“输入列”选项卡，可以在此选项卡中更改输出列的名称。 在左侧树视图中，展开“数据流目标输入”  ，然后展开“输入列” 。 在右窗格中单击输入列名称并更改输出列名称。  
  
## 另请参阅  
 [数据流目标](../../integration-services/data-flow/data-streaming-destination.md)   
 [演练：将 SSIS 包作为 SQL 视图发布](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
  