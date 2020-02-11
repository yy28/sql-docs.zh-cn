---
title: srv_rpcname（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcname
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcname
ms.assetid: 0a1424e4-3319-4836-b8d8-5e0344cc683f
author: rothja
ms.author: jroth
ms.openlocfilehash: 48ff48b18cc945754b91dc14294569040b1e73fd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005533"
---
# <a name="srv_rpcname-extended-stored-procedure-api"></a>srv_rpcname（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回当前远程存储过程的过程名称部分。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBCHAR * srv_rpcname (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
```  
  
## <a name="arguments"></a>参数  
 *srvproc*  
 指向作为特定客户端连接句柄（在这里为接收远程存储过程的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *长度*  
 指向接收数据库名称长度的整型变量的指针。 如果 len 为 NULL，则不返回远程存储过程名称的长度**。  
  
## <a name="returns"></a>返回  
 一个 DBCHAR 指针，指向当前远程存储过程的远程存储过程名称部分的以 NULL 值结束的字符串。 如果当前无远程存储过程，则返回 NULL，且 len 设置为 -1**。  
  
## <a name="remarks"></a>备注  
 此函数只返回远程存储过程的名称。 不包括所有者、数据库名称和远程存储过程编号的可选说明符。  
  
 由于在无远程存储过程的情况下也可以调用 srv_rpcname（不会出现信息性错误），因此，该函数也可用于确定是否存在远程存储过程****。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
