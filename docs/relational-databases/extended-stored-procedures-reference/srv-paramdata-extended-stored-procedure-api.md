---
title: srv_paramdata（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramdata
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramdata
ms.assetid: 3104514d-b404-47c9-b6d7-928106384874
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f8a7f5ebb1b85740735c6070a784423b3258012
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064031"
---
# <a name="srv_paramdata-extended-stored-procedure-api"></a>srv_paramdata（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回远程存储过程调用参数的值。 此函数已被 srv_paraminfo 函数取代****。  
  
## <a name="syntax"></a>语法  
  
```  
  
void * srv_paramdata (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>参数  
 *srvproc*  
 指向作为特定客户端连接句柄（在这里为接收远程存储过程调用的句柄）的 SRV_PROC 结构的指针。 该结构包含扩展存储过程库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *n*  
 表示参数的编号。 第一个参数的编号为 1。  
  
## <a name="returns"></a>返回  
 一个指向参数值的指针。 如果第 n 个参数为 NULL，则没有第 n 个参数，或者没有任何远程存储过程，并返回 NULL****。 如果参数值为字符串，则不能以 Null 值结束。 使用 srv_paramlen 确定字符串的长度****。  
  
 如果参数是[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型之一，则此函数返回以下值。 指针数据包括数据类型的指针是否为有效 (VP)、NULL 或不适用 (N/A)，以及指向的数据内容。  
  
|新数据类型|输入数据长度|  
|--------------------|-----------------------|  
|BITN|**空：** VP、NULL<br /><br /> **零：** VP、NULL<br /><br /> **>= 255：** 不适用<br /><br /> **<255：** 不适用|  
|BIGVARCHAR|**空：** NULL、N/A<br /><br /> **零：** VP、NULL<br /><br /> **>= 255：** VP，255个字符<br /><br /> **<255：** 实际数据的 VP|  
|BIGCHAR|**空：** NULL、N/A<br /><br /> **零：** VP，255空间<br /><br /> **>= 255：** VP，255个字符<br /><br /> **<255：** VP、实际数据加上填充（最多255）|  
|BIGBINARY|**空：** NULL、N/A<br /><br /> **零：** VP，255 0x00<br /><br /> **>= 255：** VP，255字节<br /><br /> **<255：** VP、实际数据加上填充（最多255）|  
|BIGVARBINARY|**空：** NULL、N/A<br /><br /> **零：** VP、0x00<br /><br /> **>= 255：** VP，255字节<br /><br /> **<255：** 实际数据的 VP|  
|NCHAR|**空：** NULL、N/A<br /><br /> **零：** VP，255空间<br /><br /> **>= 255：** VP，255个字符<br /><br /> **<255：** VP、实际数据加上填充（最多255）|  
|NVARCHAR|**空：** NULL、N/A<br /><br /> **零：** VP、NULL<br /><br /> **>= 255：** VP，255个字符<br /><br /> **<255：** 实际数据的 VP|  
|NTEXT|**空：** 不适用<br /><br /> **零：** 不适用<br /><br /> **>= 255：** 不适用<br /><br /> ** \<255：** 不适用|  
  
 
  \*   数据不能以 Null 值结束；截断 255 个字符以外的字符时不会发出警告。  
  
## <a name="remarks"></a>备注  
 如果知道参数名称，则可以使用 srv_paramnumber 获取参数编号****。 要确定参数是否为 NULL，请使用 srv_paramlen****。  
  
 使用参数执行远程存储过程调用时，可以通过名称或位置（未命名）来传递参数。 如果使用部分按名称传递，部分按位置传递的参数调用远程存储过程，则会发生错误。 如果出现错误，仍然会调用 SRV_RPC 处理程序，但是它看起来没有参数并且 srv_rpcparams 返回 0****。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [扩展存储过程 API srv_rpcparams &#40;&#41;](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
