---
title: srv_rpcparams（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcparams
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcparams
ms.assetid: 96a5e6f6-d320-4623-b96e-0a856e3abebb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 83f1368984737759eb64a5feaf31bd1ac7c79e37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62740662"
---
# <a name="srv_rpcparams-extended-stored-procedure-api"></a>srv_rpcparams（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回当前远程存储过程的参数个数。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_rpcparams ( SRV_PROC *  
srvproc   
);  
  
```  
  
## <a name="arguments"></a>参数  
 *srvproc*  
 指向作为特定客户端连接句柄（在这里为接收远程存储过程的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
## <a name="returns"></a>返回  
 远程存储过程中的参数个数。 如果远程存储过程中没有参数，或没有当前远程存储过程，则返回 -1，并发生信息错误。  
  
## <a name="remarks"></a>备注  
 该函数返回当前远程存储过程中的参数个数。 通常是从远程存储过程调用该函数。  
  
 使用参数调用远程存储过程时，可以按名称或位置（未命名）传递参数。 如果进行远程存储过程调用时，一些参数按名称传递而另一些按位置传递，则会出现错误。 发生该错误时，将调用远程存储过程处理程序，但它不接收参数，并且 srv_rpcparams 返回 0****。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
