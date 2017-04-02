---
title: "Invoke-ProcessPartition cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 516fab44-734e-425b-9bd0-b4aee1fd338f
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Invoke-ProcessPartition cmdlet
  使用特定的处理类型变量处理分区。  
  
## 语法  
 `Invoke-ProcessPartition [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [-CubeName] <System.String> [-MeasureGroupName] <System.String> [<CommonParameters>]`  
  
 `Invoke-ProcessPartition –DatabasePartition <Microsoft.AnalysisServices.Partition> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## Description  
 Invoke-ProcessParition cmdlet 为给定的多维数据集和度量值组处理 Analysis Services 数据库的特定分区。 ProcessType 值将确定操作的作用域。 处理分区时，您必须指定处理类型。 有关详细信息，请参阅[处理选项和设置 (Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
## Parameters  
  
### -Name \<string>  
 指定要处理的分区。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### -Database \<string>  
 指定多维数据集属于的数据库。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### -CubeName \<string>  
 指定度量值组所属的多维数据集。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|2|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### -MeasureGroupName \<string>  
 指定分区所属的度量值组。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|2|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### -DatabasePartition \<Microsoft.AnalysisServices.Partition>  
 指定要处理的分区。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|2|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### -ProcessType \<Microsoft.AnalysisServices.ProcessType>  
 指定处理类型：ProcessFull、ProcessAdd、ProcessUpdate、ProcessIndexes、ProcessData、ProcessDefault、ProcessClear、ProcessStructure、ProcessCelarStructureOnly、ProcessScriptCache、ProcessRecalc。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### \<CommonParameters>  
 此 cmdlet 支持以下常用参数：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## 输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|InclusionThresholdSetting|  
|输出|InclusionThresholdSetting|  
  
## 示例 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\Sales Orders\Partitions\Total_Orders_2004 > Get-Item .| Invoke-ProcessPartition –ProcessType:ProcessDefault`  
  
 此命令通过管道传入要处理的分区的标识。  
  
## 示例 2  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups> Invoke-ProcessPartition –Name “Total_Orders_2003” –MeasureGroupname “Sales Order” –CubeName “Adventure Works” –database “AWTEST” –ProcessType “ProcessFull”`  
  
 此命令将在 AWTEST 数据库的 Sales Orders 度量值组中处理分区 Total_Orders_2003。  
  
## 另请参阅  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [使用 PowerShell 管理表格模型](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  