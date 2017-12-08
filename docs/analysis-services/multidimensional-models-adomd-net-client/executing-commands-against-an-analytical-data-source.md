---
title: "对分析数据源执行命令 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- AdomdCommand object
- commands [ADOMD.NET]
- ADOMD.NET, commands
ms.assetid: 1a958e5f-fc18-480b-9706-fc44e3b1d534
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 450d3553509ee3358711705bbc3f5e8a10874820
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="executing-commands-against-an-analytical-data-source"></a>对分析数据源执行命令
  在建立与分析数据源的连接后，可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象对该数据源运行命令并从中返回结果。 这些命令可使用多维表达式 (MDX)、数据挖掘扩展插件 (DMX) 甚至是有限 SQL 语法来检索数据。 此外，您还可以使用 Analysis Services 脚本语言 (ASSL) 命令修改基础数据库。  
  
## <a name="creating-a-command"></a>创建命令  
 必须先创建命令，然后才能运行该命令。 可使用下列两种方法之一创建命令：  
  
-   第一种方法是使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 构造函数（可在数据源运行命令）和 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象（运行命令的对象）。  
  
-   第二种方法是使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.CreateCommand%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 方法。  
  
 可使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.CommandText%2A> 属性查询和修改要运行的命令的文本。 您创建的命令无需在运行后返回数据。  
  
## <a name="running-a-command"></a>运行命令  
 创建 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 对象后，有多个 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 方法，可供您的命令执行各种操作。 下表列出了其中的部分操作。  
  
|若要|方法|  
|--------|---------------------|  
|将结果作为数据流返回|使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> 以返回一个 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 对象|  
|返回一个 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 对象|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A>|  
|运行不返回行的命令|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteNonQuery%2A>|  
|返回**XMLReader**对象，其中包含的 XML for Analysis (XMLA) 兼容的格式中的数据|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>|  
  
### <a name="example-of-running-a-command"></a>运行命令示例  
 此示例使用<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>运行的 XMLA 命令时，将处理**Adventure Works DW**在本地服务器上，而无需返回数据的多维数据集。  
  
 [!code-cs[Adomd.NetClient#ExecuteXMLAProcessCommand](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/executing-commands-again_1.cs)]  
  
  
