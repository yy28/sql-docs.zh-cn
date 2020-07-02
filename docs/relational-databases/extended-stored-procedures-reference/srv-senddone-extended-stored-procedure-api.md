---
title: srv_senddone（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_senddone
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_senddone
ms.assetid: 1fc4f1d5-56d4-43f6-b5e4-0c0cc295cba3
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b5f7722daf7ebbdda988cf3fb41ac1ab5b06049
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755858"
---
# <a name="srv_senddone-extended-stored-procedure-api"></a>srv_senddone（扩展存储过程 API）
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 将结果完成消息发送到客户端。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_senddone (  
SRV_PROC *  
srvproc  
,  
DBUSMALLINT   
status  
,  
DBUSMALLINT  
info  
,  
DBINT  
count   
);  
  
```  
  
## <a name="arguments"></a>自变量  
 srvproc**  
 指向作为特定客户端连接句柄（在这里为接收语言请求的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *status*  
 各种 status 标志的 2 字节字段**。 通过与 status 标志值一起使用 AND 和 OR 逻辑运算符，可以设置多个标志**。 下表列出了可能的 status 标志**。  
  
|状态标志|描述|  
|-----------------|-----------------|  
|SRV_DONE_COUNT|count 参数包含有效计数**。|  
|SRV_DONE_ERROR|当前客户端命令收到了错误。|  
  
 *信息*  
 保留的 2 字节字段。 将该值设置为 0。  
  
 *计数*  
 用于指示当前结果集的计数的 4 字节字段。 如果在 status 字段中设置 SRV_DONE_COUNT 标志，则 count 将保存有效计数****。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL  
  
## <a name="remarks"></a>备注  
 客户端请求会导致服务器执行许多命令和返回许多结果集。 对于每个结果集，srv_senddone 必须将结果完成消息返回到客户端****。  
  
 count 字段指示受命令影响的行数**。 如果 count 字段包含计数，则应在 status 字段中设置 SRV_DONE_COUNT 标志****。 客户端通过该设置可区分等于 0 的 count 值和未使用的 count 字段****。  
  
 请勿从 SRV_CONNECT 处理程序调用 srv_senddone****。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
