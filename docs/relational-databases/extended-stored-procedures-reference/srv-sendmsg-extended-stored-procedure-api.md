---
title: srv_sendmsg（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_sendmsg
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_sendmsg
ms.assetid: efcb50b9-f8ff-4121-bf67-05830171b928
author: rothja
ms.author: jroth
ms.openlocfilehash: 757712cd6e390c4369cea08aa7d0e59d727b7d39
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755843"
---
# <a name="srv_sendmsg-extended-stored-procedure-api"></a>srv_sendmsg（扩展存储过程 API）
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 向客户端发送消息。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_sendmsg (  
SRV_PROC *  
srvproc  
,  
int  
msgtype  
,  
DBINT  
msgnum  
,  
DBTINYINT  
class  
,   
DBTINYINT  
state  
,  
DBCHAR *  
rpcname  
,  
int   
rpcnamelen  
,  
DBUSMALLINT  
linenum  
,  
DBCHAR *  
message  
,  
int  
msglen   
);  
```  
  
## <a name="arguments"></a>自变量  
 srvproc**  
 指向作为特定客户端连接句柄（在这里为接收语言请求的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 msgtype**  
 SRV_MSG_INFO 或 SRV_MSG_ERROR，具体取决于服务器发送的是信息性消息还是错误消息。  
  
 msgnum**  
 4 字节消息编号。  
  
 *class*  
 指定错误严重性。 严重性小于或等于 10 将被视为信息性消息。  
  
 State   
 提供当前消息的错误状态编号。 错误状态编号提供有关错误上下文的信息。 有效的状态编号介于 0 到 255 之间。  
  
 rpcname**  
 当前不受支持。  
  
 rpcnamelen**  
 当前不受支持。  
  
 linenum**  
 消息应用到的语言命令批处理中的行号。 行号从 1 开始。 如果 linenum 不适用于消息，则设置为 0**。  
  
 *message*  
 指向要发送到客户端的字符串的指针。  
  
 msglen**  
 指定消息的长度（以字节为单位）**。 如果消息以 null 值结束，则将 msglen 设置为 SRV_NULLTERM****。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL  
  
## <a name="remarks"></a>备注  
 此函数向客户端发送错误或信息性消息。 每一要发送的消息都调用一次该函数。  
  
 可以在使用 srv_sendrow 发送所有行（如果有）之前或之后，使用 srv_sendmsg 以任意顺序向客户端发送消息********。 在使用 srv_senddone 发送完成状态之前，所有消息（如果有）都必须发送到客户端****。  
  
 如果通过 Unicode 发送消息，请使用 srv_wsendmsg 而不是 srv_sendmsg********。  
  
 有关详细信息，请参阅 [Unicode 数据和服务器代码页](../../relational-databases/extended-stored-procedures-programming/unicode-data-and-server-code-pages.md)。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
