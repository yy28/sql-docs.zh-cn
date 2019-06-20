---
title: 启动 sqlcmd 实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1ec91705dfb9194f42c079cb7b3d5100c9d396
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090111"
---
# <a name="start-the-sqlcmd-utility"></a>启动 sqlcmd 实用工具
  开始使用 `sqlcmd` 之前，必须先启动该实用工具并连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一个实例。 可以连接到默认实例，也可以连接到命名实例。 第一步是启动 `sqlcmd` 实用工具。  
  
> [!NOTE]  
>  Windows 身份验证是 `sqlcmd` 的默认身份验证模式。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则必须使用 **-U** 和 **-P** 选项指定用户名和密码。  
  
> [!NOTE]  
>  默认情况下， [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 会安装为命名实例 **sqlexpress**。  
  
 如果之前您尚未连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例，则可能需要将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为接受连接。  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>若要启动 sqlcmd 实用工具并连接到 SQL Server 的默认实例  
  
1.  在 **“开始”** 菜单上，单击 **“运行”** 。 在 **“打开”** 框中，键入 **cmd**，然后单击 **“确定”** 打开命令提示符窗口。  
  
2.  在命令提示符下键入 `sqlcmd`。  
  
3.  按 Enter。  
  
     现在，您已与计算机上运行的默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例建立了可信连接。  
  
     **1 >** 是`sqlcmd`提示符，可以指定行号。 每按一次 Enter，该数字就会加 1。  
  
4.  若要结束`sqlcmd`会话中，键入`EXIT`在`sqlcmd`提示符。  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>若要启动 sqlcmd 实用工具并连接到 SQL Server 的命名实例  
  
1.  打开命令提示符窗口，然后键入`sqlcmd -S` *myServer\instanceName*。 使用计算机名称和要连接的 *的实例替换* myServer\instanceName [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  按 Enter。  
  
     `sqlcmd`提示符 (1 >) 表示你已连接到的指定实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    > [!NOTE]  
    >  输入的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句存储在缓冲区中。 在遇到 GO 命令时，它们将作为批处理命令执行。  
  
## <a name="see-also"></a>请参阅  
 [使用 sqlcmd 运行 Transact-SQL 脚本文件](sqlcmd-run-transact-sql-script-files.md)  
  
  
