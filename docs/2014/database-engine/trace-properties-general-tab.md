---
title: 跟踪属性 （常规选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.traceproperties.general.f1
helpviewer_keywords:
- Trace Properties dialog box
ms.assetid: 25227268-143b-477e-aac9-8268bcaf2078
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 35e9ee16ee50d5dc697e862b2777db7f0199970d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48184777"
---
# <a name="trace-properties-general-tab"></a>跟踪属性（“常规”选项卡）
  使用 **“跟踪属性”** 对话框中的 **“常规”** 选项卡可以查看或指定跟踪属性。  
  
## <a name="options"></a>选项  
 **跟踪名称**  
 指定跟踪的名称。  
  
 **跟踪提供程序名称**  
 显示要跟踪的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的名称。 将使用连接时指定的服务器的名称自动填充此字段。 若要更改跟踪提供程序的名称，请单击 **“取消”** 关闭该对话框，然后启动新的跟踪。  
  
 **跟踪提供程序类型**  
 显示提供跟踪的服务器类型。 跟踪定义文件将自动填充 **“跟踪提供程序类型”** 字段。 您无法修改此字段。  
  
 **version**  
 显示提供跟踪的服务器的版本。 跟踪定义文件将自动填充 **“版本”** 字段。 您无法修改此字段。  
  
 **使用模板**  
 从模板目录中选择一个模板。 将使用默认模板和为当前跟踪提供程序类型创建的任何用户定义模板来填充该目录。  
  
 **保存到文件**  
 将跟踪数据捕获到 .trc 文件。 保存跟踪数据有助于以后进行查看和分析。  
  
 **设置最大文件大小(MB)**  
 如果选择将跟踪数据保存到文件，则必须指定跟踪文件的最大大小。 默认值为 5 MB。 最大大小仅受保存该文件的文件系统（NTFS、FAT）的限制。  
  
 \<图形 >**另存为**  
 在选择进行保存后，可以选择此图标来更改文件名。  
  
 **启用文件滚动更新**  
 选择此选项允许在达到最大文件大小时创建其他文件来接受跟踪数据。 每个新文件名都由原始 .trc 文件名按顺序编号而成。 例如，当 **NewTrace.trc** 达到最大文件大小时，将关闭该文件，并打开一个新文件 **NewTrace_1.trc**，在新文件达到最大文件大小时将打开 **NewTrace_2.trc**，依此类推。 默认情况下，在将跟踪保存到文件时将启用文件滚动更新。  
  
 **服务器处理跟踪数据**  
 指定由运行跟踪的服务器来处理跟踪数据。 使用此选项可降低跟踪所需的性能开销。 如果选中此复选框，即使在高负荷环境下也不会跳过任何事件。 如果清除此复选框，则由 SQL Server Profiler 执行处理任务，在高负荷环境下可能不会跟踪某些事件。  
  
 **保存到表**  
 将跟踪数据捕获到数据库表。 保存跟踪数据有助于以后进行查看和分析。 但是，将跟踪数据保存到表会导致在保存跟踪的服务器上产生很大的开销。 如果可能，请不要将跟踪表保存到正在跟踪的同一服务器上。  
  
 \<图形 >**目标表**  
 在选择将跟踪数据保存到数据库表后，可以选择此图标来更改表名称。  
  
 **设置最大行数(千行)**  
 指定保存数据的最大行数。 默认值为 1000 行。  
  
 **启用跟踪停止时间**  
 为跟踪设置日期和时间，以便到时候终止并关闭此跟踪。  
  
## <a name="see-also"></a>请参阅  
 [创建跟踪 (SQL Server Profiler)](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
