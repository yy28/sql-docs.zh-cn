---
title: 检查正在使用的文件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ccd65867-d4c0-43b2-8361-7fd41c6f79ac
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34b51b26454766498ee601baae3ccc52cd1c5768
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096533"
---
# <a name="check-files-in-use"></a>检查正在使用的文件
  若要避免在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新后重新启动 Windows，请使用“检查正在使用的文件”页来识别锁定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新安装程序所需文件的进程。  
  
 停止与正在更新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例连接的所有应用程序和服务。 包括停止 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
 如果安装程序确定在安装过程中文件已被锁定，那么，您在安装完成后可能必须重新启动计算机。 如有必要，安装程序会提示您重新启动计算机。 如果安装程序必须在安装过程中停止某个服务，则在安装完成后将重新启动这个服务。  
  
 为了使安装后无需重新启动计算机，安装程序将显示正在锁定文件的进程的列表。 停止或结束列表中的进程和应用程序。 然后，单击 **“刷新检查”** 重新运行相应检查。 单击 **“停职检查”** 结束正在运行的检查。 如果找不到锁定的文件，则该表为空。 关闭或停止所有锁定的进程以后，单击 **“下一步”** 继续。  
  
 安装程序将信息记录在日志文件中。 有关如何查看日志文件的详细信息，请参阅 [查看和读取 SQL Server 安装日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md) 和 [如何读取 SQL Server 安装日志文件](https://go.microsoft.com/fwlink/?LinkID=134490)。  
  
 日志文件中包括下列信息：  
  
-   进程的名称  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的名称  
  
-   进程类型  
  
-   运行进程的帐户  
  
-   进程 ID  
  
-   锁定的文件的名称  
  
## <a name="uielement-list"></a>UIElement 列表  
  
|名称|说明|  
|----------|-----------------|  
|进程|显示以下进程的全名，该进程正在使用要更新的文件。|  
|类型|显示进程的类型。|  
|帐户|显示运行进程的帐户。|  
|进程 ID|显示进程 ID。|  
  
  
