---
title: "打开、查看和打印死锁文件 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deadlocks [SQL Server], printing files
- deadlocks [SQL Server], opening files
- opening deadlock files
- printing deadlock files
ms.assetid: 5061b13f-2cb7-457a-b8d0-fbd437b510ab
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9c77238f4fe5aa1c9078acd9d4a691c4242f4ce9
ms.lasthandoff: 04/11/2017

---
# <a name="open-view-and-print-a-deadlock-file-sql-server-management-studio"></a>打开、查看和打印死锁文件 (SQL Server Management Studio)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 生成死锁时，您可以捕获死锁信息并将死锁信息保存到文件。 保存死锁文件后，可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中将其打开以进行查看或打印。  
  
### <a name="to-open-and-view-a-deadlock-file"></a>打开和查看死锁文件  
  
1.  在 **中的** “文件” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]菜单上，指向 **“打开”**，然后单击 **“文件”**。  
  
2.  在 **“打开文件”** 对话框的 **“文件类型”** 框中选择 .xdl 文件类型。 现在，您将获得一个经过筛选的只包含死锁文件的列表。  
  
### <a name="to-print-a-deadlock-file"></a>打印死锁文件  
  
1.  在 **中的** “文件” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]菜单上，指向 **“打开”** ，然后单击 **“文件”**。  
  
2.  在 **“打开文件”** 对话框的 **“文件类型”** 框中选择 .xdl 文件类型。 现在，您将获得一个经过筛选的只包含死锁文件的列表。  
  
3.  选择要打印的死锁文件，然后单击 **“打开”**。  
  
4.  在 **“文件”** 菜单上，单击 **“打印”**。  
  
## <a name="see-also"></a>另请参阅  
 [保存死锁图形 (SQL Server Profiler)](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
  
