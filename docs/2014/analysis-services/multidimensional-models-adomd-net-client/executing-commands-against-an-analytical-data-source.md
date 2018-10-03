---
title: 对分析数据源执行命令 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- AdomdCommand object
- commands [ADOMD.NET]
- ADOMD.NET, commands
ms.assetid: 1a958e5f-fc18-480b-9706-fc44e3b1d534
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6f37e3fe4cccfbfc8824971881c7d5fb68240252
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117341"
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
|返回 `XMLReader` 对象，该对象包含以 XML for Analysis (XMLA) 兼容的格式表示的数据|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>|  
  
### <a name="example-of-running-a-command"></a>运行命令示例  
 此示例使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 运行 XMLA 命令，该命令将处理本地服务器上的 `Adventure Works DW` 多维数据集，且不返回数据。  
  
 [!code-csharp[Adomd.NetClient#ExecuteXMLAProcessCommand](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#executexmlaprocesscommand)]  
  
  
