---
title: 创建扩展存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- warnings [SQL Server]
- extended stored procedures [SQL Server], debugging
- extended stored procedures [SQL Server], creating
- messages [SQL Server], extended stored procedures
ms.assetid: 9f7c0cdb-6d88-44c0-b049-29953ae75717
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0d0343113b350c48cbc42ec5b79bbd0b849f2860
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749069"
---
# <a name="creating-extended-stored-procedures"></a>创建扩展存储过程
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 扩展存储过程是带有原型的函数：  
  
 SRVRETCODE *xp_extendedProcName* **(** SRVPROC **\*);**  
  
 使用前缀 xp_ 是可选的。 当在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中引用扩展存储过程名称时，名称区分大小写，而与服务器上安装的代码页/排序顺序无关。 当您生成 DLL 时：  
  
-   如果入口点是必需的，则编写 DllMain 函数。  
  
     此函数是可选的；如果您在源代码中未提供此函数，则编译器将链接其自己的版本，此时它仅返回 TRUE。 如果您提供了 DllMain 函数，当线程或进程附加到 DLL 或从 DLL 分离时，操作系统将调用此函数。  
  
-   必须导出从 DLL 外部调用的所有函数（所有扩展存储过程函数）。  
  
     可以通过列出其.def 文件的 EXPORTS 部分中的名称导出函数也可以使用 __declspec （dllexport），一个 Microsoft 编译器扩展名的源代码中的函数名称 (请注意， \__declspec() 以两个下划线开头)。  
  
 创建扩展存储过程 DLL 时需要这些文件。  
  
|文件|Description|  
|----------|-----------------|  
|Srv.h|扩展存储过程 API 头文件|  
|Opends60.lib|Opends60.dll 的导入库|  
  
 若要创建扩展存储过程 DLL，请创建一个类型为动态链接库的项目。 有关创建 DLL 的详细信息，请参阅开发环境文档。  
  
 强烈建议所有扩展存储过程 DLL 都实现和导出以下函数：  
  
```  
__declspec(dllexport) ULONG __GetXpVersion()  
{  
   return ODS_VERSION;  
}  
```  
  
> [!NOTE]  
>  __declspec(dllexport) 是 Microsoft 特定的编译器扩展名。 如果您的编译器不支持此指令，则应在 DEF 文件的 EXPORTS 部分之下导出此函数。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]开始使用跟踪标志-t260 开始，或者如果具有系统管理员特权的用户运行 DBCC TRACEON (260)，并且如果扩展存储过程 DLL 不支持 __getxpversion （），一条警告消息 (错误 8131:扩展存储的过程 DLL '%' 不导出\__GetXpVersion().) 打印到错误日志。 (请注意， \__GetXpVersion() 以两个下划线开头。)  
  
 如果扩展存储过程 DLL 导出 __GetXpVersion()，但函数返回的版本低于服务器所要求的版本，则会向错误日志中打印一条警告消息，其中说明函数返回的版本和服务器预期的版本。 如果收到此消息，您要返回不正确的值从\__GetXpVersion()，或您正在使用早的 srv.h 版本进行编译。  
  
> [!NOTE]  
>  SetErrorMode 是一个 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Win32 函数，不应在扩展存储过程中调用它。  
  
 建议长时间运行的扩展存储过程应定期调用 srv_got_attention，以便在连接终止或批处理中止时此过程可以终止自身。  
  
 若要调试扩展存储过程 DLL，请将其复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Binn 目录。 若要为调试会话指定可执行文件，请输入路径和文件名的名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可执行文件 (例如，C:\Program Files\Microsoft SQL Server\MSSQL12。MSSQLSERVER\MSSQL\Binn\Sqlservr.exe)。 有关 sqlservr 参数的信息，请参阅[sqlservr 应用程序](../../tools/sqlservr-application.md)。  
  
## <a name="see-also"></a>请参阅  
 [srv_got_attention&#40;扩展存储过程 API&#41;](../extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)  
  
  
