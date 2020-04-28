---
title: 启动 sqlcmd 实用工具
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80f8f63b4ddb3e8641ef503a615d57c63be35164
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "75243269"
---
# <a name="start-the-sqlcmd-utility"></a>启动 sqlcmd 实用工具
  开始使用 `sqlcmd` 之前，必须先启动该实用工具并连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一个实例。 可以连接到默认实例，也可以连接到命名实例。 第一步是启动 `sqlcmd` 实用工具。  
  
> [!NOTE]  
>  Windows 身份验证是 `sqlcmd` 的默认身份验证模式。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则必须使用 **-U** 和 **-P** 选项指定用户名和密码。  
  
> [!NOTE]  
>  默认情况下， [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 会安装为命名实例 **sqlexpress**。  
  
 如果之前您尚未连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例，则可能需要将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为接受连接。  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>启动 sqlcmd 实用工具并连接到 SQL Server 的默认实例  
  
1.  在 **“开始”** 菜单上，单击 **“运行”**。 在 **“打开”** 框中，键入 **cmd**，然后单击 **“确定”** 打开命令提示符窗口。  
  
2.  在命令提示符下键入 `sqlcmd`。  
  
3.  按 Enter。  
  
     现在，您已与计算机上运行的默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例建立了可信连接。  
  
     **1>** 是指定`sqlcmd`行号的提示。 每按一次 Enter，该数字就会加 1。  
  
4.  若要结束`sqlcmd`会话，请`EXIT`在`sqlcmd`提示符下键入。  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>启动 sqlcmd 实用工具并连接到的命名实例 SQL Server  
  
1.  打开 "命令提示符" 窗口，然后`sqlcmd -S`键入 " *myServer\instanceName*"。 使用计算机名称和要连接的 *的实例替换* myServer\instanceName [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  按 Enter。  
  
     `sqlcmd` Prompt （1>）指示你已连接到的指定实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    > [!NOTE]  
    >  输入的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句存储在缓冲区中。 在遇到 GO 命令时，它们将作为批处理命令执行。  
  
## <a name="see-also"></a>另请参阅  
 [使用 sqlcmd 运行 Transact-SQL 脚本文件](sqlcmd-run-transact-sql-script-files.md)  
  
  
