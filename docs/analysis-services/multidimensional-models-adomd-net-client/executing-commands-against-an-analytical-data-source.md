---
title: 对分析数据源执行命令 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2255f699edf57b1416191383b216875a7f13bb5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
  
