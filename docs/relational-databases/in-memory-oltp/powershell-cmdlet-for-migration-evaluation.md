---
title: "用于迁移评估的 PowerShell Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
caps.latest.revision: 5
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 5
---
# 用于迁移评估的 PowerShell Cmdlet
  Save-SqlMigrationReport cmdlet 工具可评估 SQL Server 数据库中多个对象的迁移适用性。 目前，它仅限于评估内存中 OLTP 的迁移适用性。 该 cmdlet 可以在提升的 Windows PowerShell 环境和 sqlps 中运行。  
  
## 语法  
  
```powershell  
Save-SqlMigrationReport [ -MigrationType OLTP ] [ -Server server -Database database [ -Object object_name ] ]  |  [ -InputObject smo_object ] -FolderPath path  
```  
  
#### Parameters  
 下表对这些参数进行了说明。  
  
|Parameters|说明|  
|----------------|-----------------|  
|MigrationType|该 cmdlet 设定为目标的迁移方案的类型。 目前，唯一的值是默认 OLTP。 可选。|  
|Server|目标 SQL Server 实例的名称。 如果未提供 -InputObject 参数，则在 Windows Powershell 环境中为强制参数。 在 SQLPS 中为可选。|  
|数据库|目标 SQL Server 数据库的名称。 如果未提供 -InputObject 参数，则在 Windows Powershell 环境中为强制参数。 在 SQLPS 中为可选。|  
|对象|目标数据库对象的名称。 可以是表或存储过程。|  
|InputObject|该 cmdlet 设定为目标的 SMO 对象。 如果未提供 -Server 和 -Database，则在 Windows Powershell 环境中为强制参数。 在 SQLPS 中为可选。|  
|FolderPath|该 cmdlet 应在其中存放所生成的报告的文件夹。 必需的。|  
  
## 结果  
 在 FolderPath 参数指定的文件夹中，将有两个文件夹名称：表和存储过程。 如果目标对象是一个表，其报表将位于表文件夹内。 否则它将在存储过程文件夹内。  
  
  