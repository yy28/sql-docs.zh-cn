---
title: 步骤 7：添加和配置 OLE DB 目标 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 89073c9da5a4cd6243bd1fcdcd53d3fa13d02bb9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138449"
---
# <a name="step-7-adding-and-configuring-the-ole-db-destination"></a>步骤 7：添加和配置 OLE DB 目标
  现在，您的包可以从平面文件源中提取数据，并将数据转换为与目标兼容的格式。 下一个任务是将已转换的数据实际加载到目标。 若要加载数据，您必须将 OLE DB 目标添加到数据流。 OLE DB 目标可以使用数据库表、视图或 SQL 命令将数据加载到各种 OLE DB 兼容的数据库中。  
  
 在此过程中，您将添加和配置 OLE DB 目标以使用以前创建的 OLE DB 连接管理器。  
  
### <a name="to-add-and-configure-the-sample-ole-db-destination"></a>添加和配置示例 OLE DB 目标  
  
1.  在“SSIS 工具箱”中，展开“其他目标”，并将“OLE DB 目标”拖到“数据流”选项卡的设计图面上。将 OLE DB 目标直接放置在“查找日期键”转换的下面。  
  
2.  单击“查找日期键”转换，并将绿色箭头拖到新添加的“OLE DB 目标”上，以便将两个组件连接在一起。  
  
3.  在“选择输入输出”对话框中，单击“输出”列表框中的“查找匹配输出”，然后单击“确定”。  
  
4.  在“数据流”设计图面上，在新添加的“OLE DB 目标”组件中单击“OLE DB 目标”，然后将名称更改为 **Sample OLE DB Destination**。  
  
5.  双击 **Sample OLE DB Destination**。  
  
6.  在“OLE DB 目标编辑器”对话框中，确保已在“OLE DB 连接管理器”框中选中 **localhost.AdventureWorksDW2012**。  
  
7.  在“表或视图的名称”框中，键入或选择 **[dbo].[FactCurrencyRate]**。  
  
8.  单击“新建”按钮以创建新表。  将脚本中表的名称更改为 **NewFactCurrencyRate**。  单击“确定” 。  
  
9. 单击“确定”后，该对话框将关闭，“表或视图的名称”将自动更改为 **NewFactCurrencyRate**。  
  
10. 单击“映射”。  
  
11. 验证 **AverageRate**、**CurrencyKey**、**EndOfDayRate** 以及 **DateKey** 输入列是否已正确映射到目标列。 如果映射了同名列，则说明映射正确。  
  
12. 单击“确定” 。  
  
13. 右键单击 **Sample OLE DB Destination** 目标，再单击“属性”。  
  
14. 在属性窗口中，验证是否`LocaleID`属性设置为**英语 （美国）** 并且`DefaultCodePage`属性设置为**1252年**。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 8：使第 1 课包更易理解](lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 目标](data-flow/ole-db-destination.md)  
  
  
