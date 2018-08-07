---
title: 启动 sqlcmd 实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: f9dd242745c9a21b51ddb9d53a2c3d90e49afb22
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39545337"
---
# <a name="sqlcmd---start-the-utility"></a>sqlcmd - 启动实用工具
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  使用 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md) ，可以在命令提示符处、在 SQLCMD 模式下的查询编辑器中、在 Windows 脚本文件中或者在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代理作业的操作系统 (Cmd.exe) 作业步骤中输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句、系统过程和脚本文件。
> [!NOTE]  
>  Windows 身份验证是 **sqlcmd**的默认身份验证模式。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则必须使用 **-U** 和 **-P** 选项指定用户名和密码。  
  
> [!NOTE]  
>  默认情况下， [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 会安装为命名实例 **sqlexpress**。  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>启动 sqlcmd 实用工具并连接到 SQL Server 的默认实例  
  
1.  在 **“开始”** 菜单上，单击 **“运行”**。 在 **“打开”** 框中，键入 **cmd**，然后单击 **“确定”** 打开命令提示符窗口。 （如果你之前未连接到此 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例，则可能需要配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以接受连接。）  
  
2.  在命令提示符下键入 **sqlcmd**。  
  
3.  按 Enter。  
  
     现在，您已与计算机上运行的默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例建立了可信连接。  
  
     **1>** 是 **sqlcmd** 提示符，可以指定行号。 每按一次 Enter，该数字就会加 1。  
  
4.  若要结束 **sqlcmd** 会话，请在 **sqlcmd** 提示符中键入 **EXIT** 。  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>启动 sqlcmd 实用工具并连接到 SQL Server 的命名实例  
  
1.  打开命令提示符窗口，键入 *sqlcmd -S***myServer\instanceName。 使用计算机名称和要连接的 *的实例替换* myServer\instanceName [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  按 Enter。  
  
     **sqlcmd** 提示符 (1>) 指示你已连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例。  
  
    > [!NOTE]  
    >  输入的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句存储在缓冲区中。 在遇到 GO 命令时，它们将作为批处理命令执行。  
  
## <a name="see-also"></a>另请参阅  
 [使用 sqlcmd 运行 Transact-SQL 脚本文件](../../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)  
  
  
