---
title: xp_cmdshell（转算-SQL） |微软文档
ms.custom: ''
ms.date: 03/30/2020
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
ms.openlocfilehash: 2ce32fc31373077418e77d31ce064d60e23f1b24
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402694"
---
# <a name="xp_cmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  生成 Windows 命令 shell 并以字符串的形式传递以便执行。 任何输出都作为文本的行返回。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>自变量  
 **'** *command_string* **'**  
 包含要传递到操作系统的命令的字符串。 *command_string*是**瓦尔查尔（8000）** 或**nvarchar（4000），** 没有违约。 *command_string*不能包含一组以上的双引号。 如果文件路径或*command_string*引用的程序名称中存在任何空格，则需要一对引号。 如果不方便使用内含的空格，则可考虑使用 FAT 8.3 文件名作为解决方法。  
  
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
  
 行在**nvarchar（255）** 列中返回。 如果使用**no_output**选项，则仅返回以下内容：  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>备注  
 **xp_cmdshell**生成的 Windows 进程具有与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务帐户相同的安全权限。  
  
 **xp_cmdshell**同步运行。 在命令 shell 命令执行完毕之前，不会将控制权返回给调用方。  
  
 xp_cmdshell**可以通过使用**基于策略的管理或执行**sp_configure**启用和禁用。 有关详细信息，请参阅[曲面区域配置](../../relational-databases/security/surface-area-configuration.md)[和xp_cmdshell服务器配置选项](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
> [!IMPORTANT]
>  如果在批处理中执行**xp_cmdshell**并返回错误，则批处理将失败。
  
## <a name="xp_cmdshell-proxy-account"></a>xp_cmdshell 代理帐户  
 当它不是**sysadmin**固定服务器角色的成员的用户调用它时 **，xp_cmdshell**使用存储在名为 **[#xp_cmdshell_proxy_account]** 的凭据中的帐户名称和密码连接到 Windows。 如果此代理凭据不存在 **，xp_cmdshell**将失败。  
  
 代理帐户凭据可以通过执行**sp_xp_cmdshell_proxy_account**创建。 此存储过程将 Windows 用户名和密码作为参数使用。 例如，以下命令为具有 Windows 密码 `SHIPPING\KobeR` 的 Windows 域用户 `sdfh%dkc93vcMt0` 创建代理凭据。  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 有关详细信息，请参阅[sp_xp_cmdshell_proxy_account&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 由于恶意用户有时尝试使用**xp_cmdshell**来提升其特权，因此默认情况下将禁用**xp_cmdshell。** 使用**sp_configure**或**基于策略的管理**启用它。 有关详细信息，请参阅 [xp_cmdshell 服务器配置选项](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
 首次启用时 **，xp_cmdshell**需要执行控制服务器权限，**并且xp_cmdshell**创建的 Windows 进程具有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与服务帐户相同的安全上下文。 服务[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]帐户通常具有比**xp_cmdshell**创建的进程执行的工作所需的权限更多。 为了提高安全性，应限制对**xp_cmdshell**的访问仅限于高特权用户。  
  
 要允许非管理员使用**xp_cmdshell**，并允许[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用权限较低的帐户的安全令牌创建子进程，请按照以下步骤操作：  
  
1.  使用进程要求的最小特权创建并自定义一个 Windows 本地用户帐户或一个域帐户。  
  
2.  使用**sp_xp_cmdshell_proxy_account**系统过程配置**xp_cmdshell**以使用该最低权限的帐户。  
  
    > [!NOTE]  
    >  您还可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**右键**单击对象资源管理器中的服务器名称的属性，以及查看**服务器代理帐户****部分的安全选项卡**来配置此代理帐户。  
  
3.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中使用主数据库执行`GRANT exec ON xp_cmdshell TO N'<some_user>';`语句，使特定的非**系统管理员**用户能够执行**xp_cmdshell**。 指定的用户必须存在于主数据库中。  
  
 现在，非管理员可以使用**xp_cmdshell**启动操作系统进程，这些进程使用您配置的代理帐户的权限运行。 具有 CONTROL SERVER 权限的用户 **（sysadmin**固定服务器角色的成员）将继续接收**xp_cmdshell**启动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的子进程的服务帐户的权限。  
  
 要确定**xp_cmdshell**在启动操作系统进程时使用的 Windows 帐户，请执行以下语句：  
  
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
EXEC master..xp_cmdshell 'dir *.exe'  
```  
  
### <a name="b-returning-no-output"></a>B. 不返回任何输出  
 以下示例使用 `xp_cmdshell` 执行命令字符串，且不向客户端返回输出。  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks', NO_OUTPUT;  
GO  
```  
  
### <a name="c-using-return-status"></a>C. 使用返回状态  
 在下面的示例中，扩展的`xp_cmdshell`存储过程还建议返回状态。 返回代码值存储在变量 `@result` 中。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [&#40;处理-SQL&#41;的一般扩展存储过程](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_cmdshell服务器配置选项](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [表面积配置](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
