---
title: 修改跟踪模板 |Microsoft 文档
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
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- modifying trace templates
- SQL Server Profiler, templates
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 08c08bd8838380ce1054e13697aa6873a8e98860
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138978"
---
# <a name="modify-trace-templates"></a>修改跟踪模板
  用户可以在运行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的本地计算机上的文件中修改保存的模板。 也可以修改从那些文件派生的模板。 修改现有模板时，可以在 **“跟踪属性”** 对话框的 **“事件选择”** 选项卡上，以最初设置属性时相同的顺序编辑事件类和数据列等模板属性。 可以添加和删除事件类和数据列，也可以对筛选进行更改。 修改模板后，将创建用户特定的模板，并且将保持原始系统模板的完整性。 有关详细信息，请参阅 [保存跟踪和跟踪模板](save-traces-and-trace-templates.md)。  
  
 如果您无法想起（或者没有保存）创建跟踪时使用的原始模板，或希望以后运行同一跟踪，则可能需要从现有的跟踪文件派生一个模板。 在使用现有跟踪时，可以查看属性，但是不能修改属性。 若要修改属性，请停止或暂停跟踪。 有关详细信息，请参阅[从跟踪文件或跟踪表派生模板 (SQL Server Profiler)](sql-server-profiler.md) 和[从正在运行的跟踪派生模板 (SQL Server Profiler)](derive-a-template-from-a-running-trace-sql-server-profiler.md)。  
  
 **创建跟踪模板**  
  
 [创建跟踪模板 (SQL Server Profiler)](create-a-trace-template-sql-server-profiler.md)  
  
 **通过跟踪模板运行跟踪**  
  
 [创建跟踪 (SQL Server Profiler)](create-a-trace-sql-server-profiler.md)  
  
 **修改跟踪模板**  
  
 [使用 SQL Server 事件探查器](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
 [使用 Transact-SQL](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
 **在跟踪模板或跟踪文件中添加或删除事件**  
  
 [使用 SQL Server 事件探查器](specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [使用 Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [启动跟踪](start-a-trace.md)  
  
  
