---
title: "配置 SQL Server 错误日志 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: aa8816e5496b3dd8689262cffdd07e246ececfb0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="scm-services---configure-sql-server-error-logs"></a>SCM 服务 - 配置 SQL Server 错误日志
  本主题介绍如何查看或修改回收 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志的方式。  
  
## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>打开“配置 SQL Server 错误日志”对话框  
  
1.  在对象资源管理器中，展开 SQL Server 的实例，展开“管理”，右键单击“SQL Server 日志”，再单击“配置”。  
  
2.  在 **“配置 SQL Server 错误日志”** 对话框中，从以下选项中进行选择。  
  
     **限制错误日志文件在回收之前的数目**  
     若选中此选项，将限制在错误日志回收前可以创建的错误日志数。 每次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时都将创建新的错误日志。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将保留前六个日志的备份，除非选中此选项并在下面指定一个不同的最大错误日志文件数。  
  
     **最大错误日志文件数**  
     指定错误日志文件回收前创建的最大错误日志文件数。 默认值为 6，即 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在回收备份日志前保留的以前备份日志的数量。  
  
  
