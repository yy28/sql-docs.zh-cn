---
title: 添加扩展存储过程到 SQL Server |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], adding
- adding extended stored procedures
- collations [SQL Server], extended stored procedures
ms.assetid: 10f1bb74-3b43-4efd-b7ab-7a85a8600a50
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b69f6ba2dd0fc6c5b3b2ce4f93e70239d8868007
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028347"
---
# <a name="adding-an-extended-stored-procedure-to-sql-server"></a>将扩展存储过程添加到 SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 包含扩展存储过程函数的 DLL 充当对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的扩展。 若要安装的 DLL，请将文件复制到的目录，例如一个包含标准[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DLL 文件 (C:\Program Files\Microsoft SQL Server\MSSQL12.0。*x*\MSSQL\Binn 默认情况下的)。  
  
 在将扩展存储过程 DLL 复制到服务器之后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员必须将 DLL 中的每个扩展存储过程函数注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 可以使用 sp_addextendedproc 系统存储过程完成该操作。  
  
> [!IMPORTANT]  
>  在将扩展存储过程添加到服务器并将执行权限授予其他用户之前，系统管理员应当对它进行彻底检查，确保它不包含有害或恶意的代码。  验证所有用户的输入。 验证之前，不要串联用户输入。 绝对不要执行根据尚未验证的用户输入构造的命令。  
  
 sp_addextendedproc 的第一个参数指定函数的名称，第二个参数指定包含该函数的 DLL 的名称。 建议指定 DLL 的完整路径。  
  
> [!IMPORTANT]  
>  升级到 SQL Server 2005 或更高版本后，未使用完整路径注册的现有 DLL 将无法工作。 若要更正该问题，请使用 sp_dropextendedproc 撤消注册 DLL，然后使用 sp_addextendedproc 注册，并指定完整路径。  
  
 在 `sp_addextendedproc` 中指定的函数名称必须与 DLL 中的函数名称完全相同，包括大小写。 例如，该命令将函数 `xp_hello,`（位于名为 `xp_hello.dll` 的 DLL 中）注册为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 扩展存储过程：  
  
```  
sp_addextendedproc 'xp_hello', 'c:\Program Files\Microsoft SQL Server\MSSQL12.0.MSSQLSERVER\MSSQL\Binn\xp_hello.dll';  
```  
  
 如果在 `sp_addextendedproc` 中指定的函数名称与 DLL 中的函数名称不完全匹配，则新名称将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册，但该名称是不可使用的。 例如，尽管`xp_Hello`注册为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]扩展存储的过程位于`xp_hello.dll`，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将不能在 DLL 中找到该函数，如果你使用`xp_Hello`更高版本调用该函数。  
  
```  
--Register the function (xp_hello) with an initial upper case  
sp_addextendedproc 'xp_Hello', 'c:\xp_hello.dll';  
  
--Use the newly registered name to call the function  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
--This is the error message  
Server: Msg 17750, Level 16, State 1, Procedure xp_Hello, Line 1  
Could not load the DLL xp_hello.dll, or one of the DLLs it references. Reason: 127(The specified procedure could not be found.).  
```  
  
 如果在 `sp_addextendedproc` 中指定的函数名称与 DLL 中的函数名称完全匹配，并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的排序规则是不区分大小写的，则用户可以使用该名称的小写和大写字母的任意组合来调用此扩展存储过程。  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will succeed in calling xp_hello  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HelLO @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
```  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的排序规则是区分大小写的，那么，如果用不同的大小写形式调用此扩展存储过程，即使它是以与 DLL 中的函数完全相同的名称和排序规则注册的，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仍将无法调用该过程。  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will result in an error  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
  
--This is the error  
Server: Msg 2812, Level 16, State 62, Line 1  
```  
  
 不需要停止和重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [sp_addextendedproc &#40;Transact SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
