---
title: 将跟踪结果保存到表 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0098c6b18e36d1d30ccc818a8f4f98f916fcb78d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163738"
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>将跟踪结果保存到表 (SQL Server Profiler)
  本主题说明如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]将跟踪结果保存到数据库表。  
  
### <a name="to-save-trace-results-to-a-table"></a>将跟踪结果保存到表  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”**，再连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。  
  
     将出现“跟踪属性”对话框。 **“跟踪属性”** 对话框。  
  
    > [!NOTE]  
    >  如果选择“建立连接后立即开始跟踪”，则不会显示“跟踪属性”对话框，而是开始跟踪。 若要关闭此设置，请在“工具”菜单上，单击“选项”，然后清除“建立连接后立即开始跟踪”复选框。  
  
2.  在 **“跟踪名称”** 框中，键入跟踪的名称，然后单击 **“保存到表”**。  
  
3.  在 **“连接到服务器”** 对话框中，连接到将包含跟踪表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。  
  
4.  在“目标表”对话框中，从“数据库”列表中选择一个数据库。  
  
5.  在 **“所有者”** 列表中，选择此跟踪的所有者。  
  
6.  在 **“表”** 列表中，键入或选择跟踪结果的表名。 单击“确定” **。**  
  
7.  在“跟踪属性”对话框中，选中“设置最大行数(以千为单位)”复选框以指定要保存的最大行数。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 事件探查器](sql-server-profiler.md)  
  
  
