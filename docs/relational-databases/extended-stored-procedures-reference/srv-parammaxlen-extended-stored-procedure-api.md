---
title: srv_parammaxlen（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- srv_parammaxlen
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_parammaxlen
ms.assetid: 49bfc29d-f76a-4963-b0e6-b8532dfda850
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f6e14f0644a58ea21e6b4e8b98006dd438d1d79b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855675"
---
# <a name="srvparammaxlen-extended-stored-procedure-api"></a>srv_parammaxlen（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回远程存储过程调用参数的最大数据长度。 此函数已被 srv_paraminfo 函数取代。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_parammaxlen (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄（在这里为接收远程存储过程调用的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *n*  
 指示参数的编号。 第一个参数是 1。  
  
## <a name="returns"></a>返回  
 参数数据的最大长度（以字节为单位）。 如果没有第 n 个参数或没有任何远程存储过程，则返回 -1。  
  
 如果参数为以下 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型之一，则此函数返回以下值。  
  
|新数据类型|输入数据长度|  
|--------------------|-----------------------|  
|**BITN**|**NULL：** 1<br /><br /> **ZERO：** 1<br /><br /> **>=255：** N/A<br /><br /> **<255：** N/A|  
|**BIGVARCHAR**|**NULL：** 255<br /><br /> **ZERO：** 255<br /><br /> **>=255：** 255<br /><br /> **<255：** 255|  
|**BIGCHAR**|**NULL：** 255<br /><br /> **ZERO：** 255<br /><br /> **>=255：** 255<br /><br /> **<255：** 255|  
|**BIGBINARY**|**NULL：** 255<br /><br /> **ZERO：** 255<br /><br /> **>=255：** 255<br /><br /> **<255：** 255|  
|**BIGVARBINARY**|**NULL：** 255<br /><br /> **ZERO：** 255<br /><br /> **>=255：** 255<br /><br /> **<255：** 255|  
|**NCHAR**|**NULL：** 255<br /><br /> **ZERO：** 255<br /><br /> **>=255：** 255<br /><br /> **<255：** 255|  
|**NVARCHAR**|**NULL：** 255<br /><br /> **ZERO：** 255<br /><br /> **>=255：** 255<br /><br /> **<255：** 255|  
|**NTEXT**|**NULL：**-1<br /><br /> **ZERO：**-1<br /><br /> **>=255：**-1<br /><br /> **\<255：**-1|  
  
## <a name="remarks"></a>Remarks  
 每个远程存储过程参数都具有实际数据长度和最大数据长度。 对于不允许使用 Null 值的标准固定长度数据类型，实际长度和最大长度相同。 对于可变长度数据类型，长度可以变化。 例如，声明为 varchar(30) 的参数可以具有长度仅为 10 个字节的数据。 该参数的实际长度为 10，最大长度为 30。 srv_parammaxlen 函数获取远程存储过程的最大数据长度。 若要获取参数的实际长度，请使用 srv_paramlen。  
  
 使用参数调用远程存储过程时，可以按名称或位置（未命名）传递参数。 如果使用部分按名称传递，部分按位置传递的参数调用远程存储过程，则会发生错误。 仍然会调用 SRV_RPC 处理程序，但是它看起来没有参数并且 srv_rpcparams 返回 0。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [srv_paraminfo（扩展存储过程 API）](../../relational-databases/extended-stored-procedures-reference/srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams（扩展存储过程 API）](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
