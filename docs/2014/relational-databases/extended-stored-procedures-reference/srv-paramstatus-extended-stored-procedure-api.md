---
title: srv_paramstatus（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- srv_paramstatus
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramstatus
ms.assetid: 86cecd45-0b09-42e9-8152-32a12a1c2b7a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1968748fb47fa666ed7f84c4971c39e652af6cb7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212627"
---
# <a name="srvparamstatus-extended-stored-procedure-api"></a>srv_paramstatus（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回特定远程存储过程调用参数的状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_paramstatus (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄（在这里为接收远程存储过程调用的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *n*  
 指示参数的编号。 第一个参数的编号为 1。  
  
## <a name="returns"></a>返回  
 包含参数的状态标志的 `int`。 目前，只有一个标志：如果位 0 设置为 1，则参数为一个返回参数。 如果没有第 n 个参数或没有任何远程存储过程，则返回 -1。  
  
## <a name="remarks"></a>备注  
 此例程返回远程存储过程调用参数的状态标志。  
  
 参数包含通过远程存储过程在客户端和应用程序之间传递的数据。 客户端可以指定某些参数作为返回参数。 这些返回参数可包含应用程序传递回客户端的值。  
  
 目前，只有一个状态标志，该标志指示参数是否为一个返回参数。  
  
 使用参数调用远程存储过程时，可以按名称或位置（未命名）传递参数。 如果使用部分按名称传递，部分按位置传递的参数调用远程存储过程，则会发生错误。 如果出现错误，仍然会调用 SRV_RPC 处理程序，但是它看起来没有参数并且 srv_rpcparams 返回 0。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>请参阅  
 [srv_rpcparams（扩展存储过程 API）](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
