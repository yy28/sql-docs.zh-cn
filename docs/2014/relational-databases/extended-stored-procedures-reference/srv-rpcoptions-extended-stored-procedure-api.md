---
title: srv_rpcoptions（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcoptions
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcoptions
ms.assetid: dbcce5d1-d5a1-4379-9597-04e43af5923d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0c97262ab6b3ee42b070511a813fcb4498b78d60
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62745816"
---
# <a name="srv_rpcoptions-extended-stored-procedure-api"></a>srv_rpcoptions（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回当前远程存储过程的运行时选项。  
  
## <a name="syntax"></a>语法  
  
```  
  
DBUSMALLINT srv_rpcoptions ( SRV_PROC *  
srvproc   
);  
  
```  
  
## <a name="arguments"></a>参数  
 srvproc**  
 指向作为特定客户端连接句柄（在这里为接收远程存储过程的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
## <a name="returns"></a>返回  
 一个位图，它包含用逻辑 OR 联接的当前远程存储过程的运行时标志。 如果无当前远程存储过程，则返回 0 并生成一条消息。  
  
## <a name="remarks"></a>备注  
 下表说明每个运行时标志。  
  
|运行时标志|说明|  
|--------------------|-----------------|  
|SRV_NOMETADATA|客户端已请求不带元数据信息的结果。 仅当客户端与实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通信时才使用此标志。 扩展存储过程 API 应用程序不能省略元数据信息。|  
|SRV_RECOMPILE|客户端已请求在执行远程存储过程前重新编译它。 此标志可能不适用于扩展存储过程 API 应用程序。|  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
