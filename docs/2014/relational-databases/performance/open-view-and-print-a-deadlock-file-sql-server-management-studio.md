---
title: 打开、查看和打印死锁文件 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], printing files
- deadlocks [SQL Server], opening files
- opening deadlock files
- printing deadlock files
ms.assetid: 5061b13f-2cb7-457a-b8d0-fbd437b510ab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 08bacd7a99e45e10163216c69057b167088441ad
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063911"
---
# <a name="open-view-and-print-a-deadlock-file-sql-server-management-studio"></a>打开、查看和打印死锁文件 (SQL Server Management Studio)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 生成死锁时，您可以捕获死锁信息并将死锁信息保存到文件。 保存死锁文件后，可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中将其打开以进行查看或打印。  
  
### <a name="to-open-and-view-a-deadlock-file"></a>打开和查看死锁文件  
  
1.  在中的 "**文件**" 菜单上 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，指向 "**打开**"，然后单击 "**文件**"。  
  
2.  在 **“打开文件”** 对话框的 **“文件类型”** 框中选择 .xdl 文件类型。 现在，您将获得一个经过筛选的只包含死锁文件的列表。  
  
### <a name="to-print-a-deadlock-file"></a>打印死锁文件  
  
1.  在 **中的** “文件” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]菜单上，指向 **“打开”** ，然后单击 **“文件”**。  
  
2.  在 **“打开文件”** 对话框的 **“文件类型”** 框中选择 .xdl 文件类型。 现在，您将获得一个经过筛选的只包含死锁文件的列表。  
  
3.  选择要打印的死锁文件，然后单击 **“打开”**。  
  
4.  在 **“文件”** 菜单上，单击 **“打印”**。  
  
## <a name="see-also"></a>另请参阅  
 [保存死锁图形 &#40;SQL Server Profiler&#41;](save-deadlock-graphs-sql-server-profiler.md)  
  
  
