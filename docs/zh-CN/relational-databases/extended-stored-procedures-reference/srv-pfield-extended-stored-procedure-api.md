---
title: srv_pfield（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_pfield
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfield
ms.assetid: a61e4c1f-e65b-48ea-a7d1-3e1544af389d
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 70e5a797f44167d079f9ef3375b591016055eb0e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="srvpfield-extended-stored-procedure-api"></a>srv_pfield（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回有关数据库连接的信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBCHAR * srv_pfield (  
SRV_PROC *  
srvproc  
,  
int   
field  
,  
int *  
len  
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 标识数据库连接的指针。  
  
 field  
 指定连接将返回的数据。  
  
|ReplTest1|返回|  
|-----------|-------------|  
|SRV_APPLNAME|客户端建立连接时提供的应用程序名称。|  
|SRV_BCPFLAG|一个标志，如果客户端正在准备执行大容量复制操作，则为 TRUE；否则为 FALSE。|  
|SRV_CLIB|使客户端能够与服务器通信的库的名称。|  
|SRV_CPID|客户端源计算机上的客户端进程 ID。|  
|SRV_HOST|客户端建立连接时提供的客户端计算机的名称。|  
|SRV_LIBVERS|客户端库的版本。|  
|SRV_LSECURE|一个标志。 如果连接使用集成安全性进行登录，则为 TRUE。|  
|SRV_NETWORK_MODULE|连接使用的网络库 DLL 的名称。|  
|SRV_NETWORK_VERSION|连接使用的网络库 DLL 的版本。|  
|SRV_NETWORK_CONNECTION|传递到用于当前 srvproc 连接的网络库 DLL 的连接字符串。|  
|SRV_PIPEHANDLE|包含某个已连接客户端的管道句柄的字符串，或者，如果客户端连接到不使用命名管道的网络，则为 NULL。 若要将此句柄用作 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 的有效管道句柄，请将此字符串转换为整数。|  
|SRV_RMTSERVER|客户端进程从中登录的服务器。 如果从客户端进行登录，则此值为空字符串。|  
|SRV_ROWSENT|srvproc 已经为当前结果集发送的行数。|  
|SRV_SPID|srvproc 的服务器线程 ID。 对于扩展存储过程，此值与 sys.sysprocesses的 kpid 列相同，并且它可能随时间的推移而发生变化。|  
|SRV_SPROC_CODEPAGE|服务器用于解释多字节数据的代码页。|  
|SRV_STATUS|srvproc 的当前状态：正在运行或已关闭|  
|SRV_TYPE|srvproc 的连接类型。 如果返回服务器，srvproc 则来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。 如果返回客户端，srvproc 则来自 DB-Library 或 ODBC 客户端。|  
|SRV_USER|连接的用户名。|  
|||  
  
 len  
 指向一个 int 变量的指针，该变量包含所返回的 field 值的长度。 如果 len 为 NULL，则不返回字符串的长度。  
  
## <a name="returns"></a>返回  
 指向一个以 null 值结束的字符串的指针，该字符串包含 SRV_PROC 结构中指定字段的当前值。 如果此字段为空，则返回指向空字符串的有效指针，并且 len 包含 0。 如果此字段为未知，则返回 NULL 并且 len 包含值 -1。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的详细信息，请访问[安全开发人员中心](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
  
