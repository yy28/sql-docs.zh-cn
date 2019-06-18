---
title: 创建针对挖掘模型内容查询 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content queries [DMX]
ms.assetid: a0ce837a-89ed-46cf-9ce1-801ccb75fa04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d2e3607426ecbc51b1d04dfc97b12f83faf328b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085574"
---
# <a name="create-a-content-query-on-a-mining-model"></a>针对挖掘模型创建内容查询
  使用 AMO 或 XML/A 可以采用编程方式查询挖掘模型内容，但是使用 DMX 创建查询更简单。 您还可以通过建立与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的连接并使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供的 DMV 创建查询，来针对数据挖掘架构行集创建查询。  
  
 下面的过程介绍如何使用 DMX 针对挖掘模型创建查询以及如何查询数据挖掘架构行集。  
  
 有关如何使用 XML/A 创建类似查询的示例，请参阅 [使用 XMLA 创建数据挖掘查询](create-a-data-mining-query-by-using-xmla.md)。  
  
## <a name="querying-data-mining-model-content-by-using-dmx"></a>使用 DMX 查询数据挖掘模型的内容  
  
#### <a name="to-create-a-dmx-model-content-query"></a>创建 DMX 模型内容查询  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“视图”  菜单上，单击“模板资源管理器”  。  
  
2.  在 **“模板资源管理器”** 窗格中，单击四方体图标，以更改列表并显示 Analysis Services 模板。  
  
3.  在模板类别列表中，展开“DMX”，再展开“模型内容”，然后双击“内容查询”    。  
  
4.  在 **“连接到 Analysis Services”** 对话框中，选择包含要查询的挖掘模型的实例，然后单击 **“连接”** 。  
  
     此时将在相应代码编辑器中打开 **“内容查询”** 模板。 元数据窗格列出了当前数据库中的可用模型。 若要更改数据库，请从 **“可用数据库”** 列表中选择不同的数据库。  
  
5.  在一行中，输入挖掘模型的名称`FROM`[ *\<挖掘模型、 名称、 MyModel >* ]`.CONTENT`。 如果挖掘模型的名称包含空格，则必须用方括号将该名称括起来。  
  
     如果不希望键入名称，则可以在 **对象资源管理器** 中选择某个挖掘模型，并将其拖放到模板中。  
  
6.  在行中， `SELECT` *\<选择列表、 expr 列表\* >* ，键入挖掘模型内容架构行集中的列的名称。  
  
     若要查看可在挖掘模型内容查询中返回的列的列表，请参阅 [挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)提供的 DMV 创建查询，来针对数据挖掘架构行集创建查询。  
  
7.  或者，您也可以在模板的 WHERE 子句中键入条件，以将返回的行限制为特定的节点或值。  
  
8.  单击 **“执行”** 。  
  
## <a name="querying-the-data-mining-schema-rowsets"></a>查询数据挖掘架构行集  
  
#### <a name="to-create-a-query-against-the-data-mining-schema-rowset"></a>对数据挖掘架构行集创建查询  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 **“新建查询”** 工具栏中，单击 **“Analysis Services DMX 查询”** 或 **“Analysis Services MDX 查询”** 。  
  
2.  在 **“连接到 Analysis Services”** 对话框中，选择包含要查询的对象的实例，然后单击 **“连接”** 。  
  
     此时将在相应代码编辑器中打开 **“内容查询”** 模板。 元数据窗格列出了当前数据库中的可用对象。 若要更改数据库，请从 **“可用数据库”** 列表中选择不同的数据库。  
  
3.  在查询编辑器中，键入以下内容：  
  
     `SELECT *`  
  
     `FROM $system.DMSCHEMA_MINING_MODEL_CONTENT`  
  
     `WHERE MODEL_NAME = '<model name>'`  
  
4.  单击 **“执行”** 。  
  
     “结果”窗格将显示模型的内容。  
  
    > [!NOTE]  
    >  若要查看当前实例的可查询的所有架构行集的列表，请使用以下查询：`SELECT * FROM $system.`DISCOVER_SCHEMA_ROWSETS。 或者，若要查看特定于数据挖掘的架构行集的列表，请参阅 [Data Mining Schema Rowsets](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)   
 [Data Mining Schema Rowsets](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
  
