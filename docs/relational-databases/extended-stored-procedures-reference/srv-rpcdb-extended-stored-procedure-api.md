---
title: srv_rpcdb（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcdb
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcdb
ms.assetid: d52bfd22-7a7c-4ab0-af65-df96ff359e6f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9cb924bbaa93322a93d77d4a5e1234ba95d4324a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63472067"
---
# <a name="srvrpcdb-extended-stored-procedure-api"></a>srv_rpcdb（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回当前远程存储过程的数据库名称部分。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBCHAR * srv_rpcdb (  
SRV_PROC * srvproc,int *len );  
```  
  
## <a name="arguments"></a>参数  
 srvproc   
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 len   
 指向接收数据库名称长度的 int 变量的指针  。 如果 len 为 NULL，则不返回数据库名称的长度  。  
  
## <a name="returns"></a>返回  
 一个 DBCHAR 指针，指向当前远程存储过程的数据库名称部分的以 NULL 值结束的字符串。 如果当前无远程存储过程，则返回 NULL，且 len 参数设置为 -1  。  
  
## <a name="remarks"></a>Remarks  
 此函数只返回远程存储过程对象名称的数据库部分。 它不包括所有者、远程存储过程名称和远程存储过程编号的可选说明符。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
  
