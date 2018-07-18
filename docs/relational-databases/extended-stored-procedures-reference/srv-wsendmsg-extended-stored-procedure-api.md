---
title: srv_wsendmsg（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_wsendmsg
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_wsendmsg
ms.assetid: f2153076-32c9-4a52-8e1b-fc9618153543
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fc68f10b6df22ed1a5be73a8f7d35e4bb871dad3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32936024"
---
# <a name="srvwsendmsg-extended-stored-procedure-api"></a>srv_wsendmsg（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 向客户端发送 Unicode 消息。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_wsendmsg(SRV_PROC *   
srvproc  
, int   
msgnum  
, int   
severity  
, WCHAR *   
message  
, int   
msglen  
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 Msgnum  
 4 字节消息编号。  
  
 *Severity*  
 指定错误的严重性。 严重性小于或等于 10 将被视为信息性消息；否则为错误消息。  
  
 message  
 指向要发送到客户端的 Unicode 字符串的指针。  
  
 msglen  
 指定消息的长度（以字符为单位）。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>Remarks  
 使用此函数以 Unicode 格式发送消息。 这类似于 srv_sendmsg，但是它发送的消息是一个 WCHAR 字符串而不是 DBCHAR 类型的字符串。 请注意，以字符而不是字节为单位报告消息长度，而且 msglen 绝不会等于 SRV_NULLTERM。  
  
 该函数在以下情况下返回 FAIL：  
  
-   给定的 msglen 不在 0-32242 范围内。  
  
-   给定的 msglen 为 0，但消息指针为 NULL。  
  
-   通过网络发送错误消息时出错。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [srv_sendmsg（扩展存储过程 API）](../../relational-databases/extended-stored-procedures-reference/srv-sendmsg-extended-stored-procedure-api.md)  
  
  
