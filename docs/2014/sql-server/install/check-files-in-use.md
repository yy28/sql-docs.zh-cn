---
title: 检查正在使用的文件 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ccd65867-d4c0-43b2-8361-7fd41c6f79ac
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 26b0f9598aa04afc9afebc90a571c999ce653821
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015836"
---
# <a name="check-files-in-use"></a>检查正在使用的文件
  若要避免在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新后重新启动 Windows，请使用“检查正在使用的文件”页来识别锁定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新安装程序所需文件的进程。  
  
 停止与正在更新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例连接的所有应用程序和服务。 包括停止 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
 如果安装程序确定在安装过程中文件已被锁定，那么，您在安装完成后可能必须重新启动计算机。 如有必要，安装程序会提示您重新启动计算机。 如果安装程序必须在安装过程中停止某个服务，则在安装完成后将重新启动这个服务。  
  
 为了使安装后无需重新启动计算机，安装程序将显示正在锁定文件的进程的列表。 停止或结束列表中的进程和应用程序。 然后，单击 **“刷新检查”** 重新运行相应检查。 单击 **“停职检查”** 结束正在运行的检查。 如果找不到锁定的文件，则该表为空。 关闭或停止所有锁定的进程以后，单击 **“下一步”** 继续。  
  
 安装程序将信息记录在日志文件中。 有关如何查看日志文件的详细信息，请参阅[查看和读取 SQL Server 安装日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)和[如何读取 SQL Server 安装日志文件](http://go.microsoft.com/fwlink/?LinkID=134490)。  
  
 日志文件中包括下列信息：  
  
-   进程的名称  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的名称  
  
-   进程类型  
  
-   运行进程的帐户  
  
-   进程 ID  
  
-   锁定的文件的名称  
  
## <a name="uielement-list"></a>UIElement 列表  
  
|“属性”|Description|  
|----------|-----------------|  
|处理|显示以下进程的全名，该进程正在使用要更新的文件。|  
|类型|显示进程的类型。|  
|帐户|显示运行进程的帐户。|  
|进程 ID|显示进程 ID。|  
  
  