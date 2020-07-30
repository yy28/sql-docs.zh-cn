---
title: srv_message_handler（扩展存储过程 API）
description: 了解 srv_message_handler 以及它如何调用已安装的扩展存储过程 API 消息处理程序。
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_message_handler
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_message_handler
ms.assetid: 41bcd057-436f-4fa8-8293-fc8057a30877
author: rothja
ms.author: jroth
ms.openlocfilehash: 2edc96558c00b43dfe9d9b346ad75c32b42af1cd
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332352"
---
# <a name="srv_message_handler-extended-stored-procedure-api"></a>srv_message_handler（扩展存储过程 API）
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 调用安装的扩展存储过程 API 消息处理程序。 此函数通常用于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 从扩展存储过程调用，以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志文件或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 应用程序日志中记录错误（由扩展存储过程定义）。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_message_handler (  
SRV_PROC *  
srvproc  
,  
int  
errornum  
,  
BYTE   
severity  
,  
BYTE  
state  
,  
int  
oserrnum  
,  
char *  
errtext  
,  
int  
errtextlen  
,  
char *  
oserrtext  
,  
int  
oserrtextlen  
);  
```  
  
## <a name="arguments"></a>自变量  
 srvproc**  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 srvproc 参数包含用于管理应用程序和客户端之间的通信和数据的信息**。  
  
 errornum**  
 由扩展存储过程定义的错误编号。 该数字必须介于 50,001 和 2,147,483,647 之间。  
  
 severity   
 错误的标准 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 严重性值。 该数字必须介于 0 和 24 之间。  
  
 State  
 错误的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 状态值。  
  
 oserrnum**  
 操作系统错误编号。 此参数忽略。  
  
 errtext**  
 扩展存储过程错误 errornum 的说明**。  
  
 errtextlen**  
 扩展存储过程错误字符串 errtext 的长度**。  
  
 oserrtext**  
 操作系统错误 oserrnum 的说明**。 此参数忽略。  
  
 oserrtextlen**  
 操作系统错误字符串 oserrtext 的长度**。  
  
## <a name="returns"></a>返回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 srv_message_handler 函数使扩展存储过程能够与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的集中错误日志记录和报告功能集成****。 可以为扩展存储过程中的事件建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 警报，SQL Server 代理将监视这些警报情况。  
  
 如果错误消息较长，则将其截断为 412 个字节。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://msdn.microsoft.com/security/)。  
  
  
