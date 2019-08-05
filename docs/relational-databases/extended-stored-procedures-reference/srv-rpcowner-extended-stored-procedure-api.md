---
title: srv_rpcowner（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcowner
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcowner
ms.assetid: e81a60e6-14ea-47bc-a11c-3d7635344447
author: rothja
ms.author: jroth
ms.openlocfilehash: 3bb52186b88b678f9abe276fb5f18f1dd7505b96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119692"
---
# <a name="srv_rpcowner-extended-stored-procedure-api"></a>srv_rpcowner（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回当前远程存储过程的所有者组件。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBCHAR * srv_rpcowner (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc   
 指向作为特定客户端连接句柄（在这里为接收远程存储过程的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 len   
 指向接收所有者名称长度的整数变量的指针。 参数 len 可为 NULL，在这种情况下不会返回所有者组件的长度  。  
  
## <a name="returns"></a>返回  
 一个 DBCHAR 指针，指向当前远程存储过程的以 Null 值结束的所有者组件。 如果当前无远程存储过程，则返回 NULL，且 len 设置为 -1  。  
  
## <a name="remarks"></a>Remarks  
 此函数只返回远程存储过程的所有者组件。 不包括名称、远程存储过程名称和远程存储过程编号的可选说明符。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
