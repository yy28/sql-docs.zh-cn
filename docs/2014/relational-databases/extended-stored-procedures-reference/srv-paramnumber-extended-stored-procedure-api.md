---
title: srv_paramnumber（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramnumber
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramnumber
ms.assetid: d7a6dbff-71d9-4297-8a4f-bfd2876fe204
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e957b4c775554869b04805f009d4daed4f1055a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127167"
---
# <a name="srv_paramnumber-extended-stored-procedure-api"></a>srv_paramnumber（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回远程存储过程调用参数的编号。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_paramnumber (  
SRV_PROC *  
srvproc  
,  
DBCHAR *  
name  
,   
int  
namelen   
);  
  
```  
  
## <a name="arguments"></a>参数  
 *srvproc*  
 指向作为特定客户端连接句柄（在这里为接收远程存储过程调用的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *路径名*  
 指向参数 name 的指针**。  
  
 *namelen*  
 name 的长度**。 如果 name 以 null 值终止，namelen 则设置为 SRV_NULLTERM****。  
  
## <a name="returns"></a>返回  
 命名参数的参数编号。 第一个参数是 1。 如果没有参数命名为 name 或没有远程存储过程，则返回 0 并生成一条消息**。  
  
## <a name="remarks"></a>备注  
 使用参数调用远程存储过程时，可以按名称或位置（未命名）传递参数。 如果使用部分按名称传递，部分按位置传递的参数调用远程存储过程，则会发生错误。 仍会调用 SRV_RPC 处理程序，但它似乎没有参数， **srv_rpcparams**返回0。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [扩展存储过程 API srv_rpcparams &#40;&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
