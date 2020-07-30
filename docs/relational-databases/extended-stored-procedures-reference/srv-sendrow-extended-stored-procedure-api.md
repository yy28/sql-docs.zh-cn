---
title: srv_sendrow（扩展存储过程 API）| Microsoft Docs
description: 在扩展存储过程 API 中了解 srv_sendrow。 srv_sendrow 将一行数据传输到客户端。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_sendrow
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_sendrow
ms.assetid: a08f608a-10e6-4bff-9b48-0d02e8026cdb
author: rothja
ms.author: jroth
ms.openlocfilehash: 1cbe5886d19ca1da9bdc2bdea09ce86d142b44d9
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248204"
---
# <a name="srv_sendrow-extended-stored-procedure-api"></a>srv_sendrow（扩展存储过程 API）
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 将一行数据传送到客户端。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_sendrow ( SRV_PROC *  
srvproc   
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc**  
 指向作为特定客户端连接句柄（在这里为接收语言请求的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 对于发送到客户端的每行调用一次 srv_sendrow 函数****。 在使用 srv_sendmsg、srv_status 或 srv_senddone 发送任何消息、状态值或完成状态之前，必须将所有行发送到客户端************。  
  
 如果发送尚未使用 srv_describe 定义其所有列的某行，则会导致扩展存储过程 API 应用程序引发信息性错误消息并向客户端返回 FAIL****。 在此情况下，将不发送该行。  
  
> [!NOTE]  
>  扩展存储过程 API 不支持将计算行发送到客户端。 此外，如果将包含 ntext、text 或 image 数据的行发送到客户端，则不会包含文本指针和文本时间戳************。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [srv_describe（扩展存储过程 API）](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
