---
title: xp_cmdshell (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b01628e339e4a3ce1f824f27edd75e2e5aea2526
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123771"
---
# <a name="xpcmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  生成 Windows 命令 shell 并以字符串的形式传递以便执行。 任何输出都作为文本的行返回。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>参数  
 **'** *command_string*   
 包含要传递到操作系统的命令的字符串。 *command_string*是**varchar(8000)** 或**nvarchar(4000)** ，无默认值。 *command_string*不能包含多个集的两个双引号。 如果任何空格都存在于文件路径或程序中引用的名称，则需要一对引号*command_string*。 如果不方便使用内含的空格，则可考虑使用 FAT 8.3 文件名作为解决方法。  
  
 **no_output**  
 可选参数，指定不应向客户端返回任何输出。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 执行以下 `xp_cmdshell` 语句将返回当前目录的目录列表。  
  
```  
EXEC xp_cmdshell 'dir *.exe';  
GO  
```  
  
 在返回的行**nvarchar(255)** 列。 如果**no_output**使用选项时，就将返回仅以下：  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>备注  
 通过生成 Windows 进程**xp_cmdshell**具有相同的安全权限作为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务帐户。  
  
 **xp_cmdshell**同步运行。 在命令 shell 命令执行完毕之前，不会将控制权返回给调用方。  
  
 **xp_cmdshell**可以启用和禁用通过使用基于策略的管理或通过执行**sp_configure**。 有关详细信息，请参阅[外围应用配置器](../../relational-databases/security/surface-area-configuration.md)并[xp_cmdshell 服务器配置选项](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
> [!IMPORTANT]
>  如果**xp_cmdshell**批处理中执行，并返回错误，批处理将失败。 这是行为的更改。 在早期版本的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]批处理将会继续执行。  
  
## <a name="xpcmdshell-proxy-account"></a>xp_cmdshell 代理帐户  
 用户不是成员的调用时**sysadmin**固定服务器角色**xp_cmdshell**使用的帐户名称和密码存储在名为的凭据连接到 Windows **# #xp_cmdshell_proxy_account # #** 。 该代理凭据不存在，如果**xp_cmdshell**将失败。  
  
 可以通过执行创建代理帐户凭据**sp_xp_cmdshell_proxy_account**。 此存储过程将 Windows 用户名和密码作为参数使用。 例如，以下命令为具有 Windows 密码 `SHIPPING\KobeR` 的 Windows 域用户 `sdfh%dkc93vcMt0` 创建代理凭据。  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 有关详细信息，请参阅[sp_xp_cmdshell_proxy_account &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 因为恶意用户有时试图通过使用其特权提升**xp_cmdshell**， **xp_cmdshell**默认处于禁用状态。 使用**sp_configure**或**基于策略的管理**来启用它。 有关详细信息，请参阅 [xp_cmdshell 服务器配置选项](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
 首次启用时， **xp_cmdshell**需要 CONTROL SERVER 权限才能执行和创建的 Windows 进程**xp_cmdshell**具有相同的安全上下文为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务帐户。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务帐户通常具有更多执行创建的进程的工作所需权限**xp_cmdshell**。 为了增强安全性，访问**xp_cmdshell**应被限制为高特权的用户。  
  
 若要允许非管理员使用**xp_cmdshell**，并允许[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要创建具有较低特权帐户的安全令牌的子进程，请执行以下步骤：  
  
1.  使用进程要求的最小特权创建并自定义一个 Windows 本地用户帐户或一个域帐户。  
  
2.  使用**sp_xp_cmdshell_proxy_account**系统过程来配置**xp_cmdshell**可将该最小特权帐户。  
  
    > [!NOTE]  
    >  此外可以配置此代理帐户使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]通过右击**属性**服务器名称在对象资源管理器中，并查看**安全**选项卡上的**服务器代理帐户**部分。  
  
3.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，使用 master 数据库执行`GRANT exec ON xp_cmdshell TO '<somelogin>'`语句，以提供特定的非**sysadmin**用户执行的能力**xp_cmdshell**。 指定的登录名必须映射到 master 数据库中的用户。  
  
 现在，非管理员可以启动操作系统进程**xp_cmdshell**和使用已配置的代理帐户的权限运行的那些进程。 具有 CONTROL SERVER 权限的用户 (成员**sysadmin**固定的服务器角色) 将继续接收的权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由启动子进程的服务帐户**xp_cmdshell**.  
  
 若要确定正在使用的 Windows 帐户**xp_cmdshell**时启动操作系统进程，请执行以下语句：  
  
```  
xp_cmdshell 'whoami.exe'  
  
```  
  
 若要确定其他登录名的安全上下文，请执行以下语句：  
  
```  
EXECUTE AS LOGIN = '<other_login>' ;  
GO  
xp_cmdshell 'whoami.exe' ;  
REVERT ;  
  
```  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-a-list-of-executable-files"></a>A. 返回可执行文件列表  
 以下示例显示执行目录命令的 `xp_cmdshell` 扩展存储过程。  
  
```  
EXEC master..xp_cmdshell 'dir *.exe''  
```  
  
### <a name="b-returning-no-output"></a>B. 不返回任何输出  
 以下示例使用 `xp_cmdshell` 执行命令字符串，且不向客户端返回输出。  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks, NO_OUTPUT';  
GO  
```  
  
### <a name="c-using-return-status"></a>C. 使用返回状态  
 在以下示例中，`xp_cmdshell`扩展存储的过程也给出返回状态。 返回代码值存储在变量 `@result` 中。  
  
```  
DECLARE @result int;  
EXEC @result = xp_cmdshell 'dir *.exe';  
IF (@result = 0)  
   PRINT 'Success'  
ELSE  
   PRINT 'Failure';  
```  
  
### <a name="d-writing-variable-contents-to-a-file"></a>D. 将变量内容写入文件中  
 以下示例将 `@var` 变量的内容写入当前服务器目录下名为 `var_out.txt` 的文件中。  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'Hello world';  
SET @cmd = 'echo ' + @var + ' > var_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
### <a name="e-capturing-the-result-of-a-command-to-a-file"></a>E. 将命令的结果捕获到文件中  
 以下示例将当前目录的内容写入当前服务器目录下名为 `dir_out.txt` 的文件中。  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'dir/p';  
SET @cmd = @var + ' > dir_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
## <a name="see-also"></a>请参阅  
 [常规扩展存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_cmdshell 服务器配置选项](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [外围应用配置器](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
