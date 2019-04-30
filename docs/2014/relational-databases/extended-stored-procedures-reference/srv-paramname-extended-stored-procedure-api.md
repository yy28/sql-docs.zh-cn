---
title: srv_paramname（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramname
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramname
ms.assetid: 1a53d707-7b06-49cc-a0df-ac727cfe953f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8a5eca5aef966d205ef550b05eff2d7055e4cb28
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127177"
---
# <a name="srvparamname-extended-stored-procedure-api"></a>srv_paramname（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回远程存储过程调用参数的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBCHAR * srv_paramname (  
SRV_PROC * srvproc,intn, int *len );  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄（在这里为接收远程存储过程调用的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *n*  
 指示参数的编号。 第一个参数是 1。  
  
 len  
 提供指向 `int` 变量的指针，该变量包含以字节为单位的参数名称的长度。 如果 len 为 NULL，则不返回远程存储过程参数名称的长度。  
  
## <a name="returns"></a>返回  
 指向包含参数名称的 Null 值结束字符串的指针。 参数名称的长度存储在 len 中。 如果没有第 n 个参数或没有远程存储过程，则返回 NULL，len 会设置为 -1，并且会发送信息性错误消息。 如果参数名称为 NULL，len 则将设置为 0，并且返回以 null 值终止的空字符串。  
  
## <a name="remarks"></a>备注  
 该函数获取远程存储过程调用参数的名称。 使用参数调用远程存储过程时，可以按名称或位置（未命名）传递参数。 如果使用部分按名称传递，部分按位置传递的参数调用远程存储过程，则会发生错误。 仍然会调用 SRV_RPC 处理程序，但是它看起来没有参数并且 srv_rpcparams 返回 0。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>请参阅  
 [srv_rpcparams（扩展存储过程 API）](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
