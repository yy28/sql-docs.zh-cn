---
title: 从跟踪文件或跟踪表派生模板 (SQL Server Profiler)| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
ms.assetid: 305817b7-4d23-49fb-9e6c-4d34359877bf
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a2fa5402abf9ad6da6d5851484dcef3f36934433
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024234"
---
# <a name="derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler"></a>从跟踪文件或跟踪表派生模板 (SQL Server Profiler)
  本主题说明如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]从现有跟踪文件或跟踪表创建跟踪模板。  
  
### <a name="to-derive-a-template-from-a-trace-file-or-trace-table"></a>从跟踪文件或跟踪表派生模板  
  
1.  打开要从其派生模板的跟踪文件或跟踪表。 有关详细信息，请参阅[打开跟踪文件 (SQL Server Profiler)](open-a-trace-file-sql-server-profiler.md) 或[打开跟踪表 (SQL Server Profiler)](open-a-trace-table-sql-server-profiler.md)。  
  
2.  在 **“文件”** 菜单上，指向 **“另存为”**，再单击 **“跟踪模板”**。  
  
3.  键入名称或从列表中选择一个名称。 单击“确定” 。  
  
> [!NOTE]  
>  如果选择现有模板文件，系统将会询问您是否希望覆盖现有文件。  
  
## <a name="see-also"></a>请参阅  
 [创建跟踪模板&#40;SQL Server 事件探查器&#41;](create-a-trace-template-sql-server-profiler.md)   
 [修改跟踪模板 (SQL Server Profiler)](../../database-engine/modify-a-trace-template-sql-server-profiler.md)   
 [从正在运行的跟踪中派生模板 (SQL Server Profiler)](derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [SQL Server 事件探查器](sql-server-profiler.md)  
  
  