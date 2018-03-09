---
title: "srv_getbindtoken（扩展存储过程 API）| Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- srv_getbindtoken
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_getbindtoken
ms.assetid: c947d011-08ac-4fb8-b925-3da6e0999277
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a7deeadc2003fa6dd4dba53e11efc2c135240696
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="srvgetbindtoken-extended-stored-procedure-api"></a>srv_getbindtoken（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 获取调用该扩展存储过程的当前客户端会话中事务的绑定令牌。  
  
 该扩展存储过程然后可以使用 sp_bindsession 将它针对同一服务器创建的任意新会话绑定到现有事务，以便新会话可以与调用了该扩展存储过程的客户端会话共享同一事务锁空间。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_getbindtoken (  
SRV_PROC*  
srvproc  
,  
char*  
bindtoken  
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的所有信息。  
  
 bindtoken  
 指向要复制绑定令牌的缓冲区的指针。 该绑定令牌用以 Null 值结束的字符串表示。 指定的缓冲区长度至少为 255 个字节。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>注释  
  
### <a name="to-bind-an-extended-stored-procedure-session-to-the-client-session-that-called-it-so-they-share-the-same-transaction-lock-space"></a>将扩展存储过程会话绑定到调用它的客户端会话以便它们共享同一事务锁空间  
  
1.  扩展存储过程调用 svr_getbindtoken 获取会话中当前事务的绑定令牌。 在给定的 bindtoken 参数中返回该令牌。  
  
2.  扩展存储过程打开针对同一服务器的新会话。 在该会话内，扩展存储过程将绑定令牌用于 sp_bindsession 以将新会话绑定到同一事务。 扩展存储过程可以创建多个会话并将所有会话绑定到同一事务。  
  
3.  当外部存储过程返回空字符串或使用空字符串调用 sp_bindsession 时，解除对会话的绑定。  
  
    > [!NOTE]  
    >  一次只能有一个绑定会话可以访问共享连接。 如果当前一个会话正在服务器上执行一个语句或其结果从服务器挂起，则在当前会话完成执行当前语句之前，其他共享同一绑定连接的会话都不能访问服务器。 如果在服务器忙时会话试图访问该连接，将为冲突的会话返回错误，指明连接正在使用中，会话应稍后重试。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [sp_bindsession &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [sp_getbindtoken (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)  
  
  
