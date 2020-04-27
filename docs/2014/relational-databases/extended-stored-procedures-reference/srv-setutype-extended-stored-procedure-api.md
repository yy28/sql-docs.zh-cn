---
title: srv_setutype（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_setutype
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2439b19c4550d07b8d50a0bed6d72b603b1601a8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62745786"
---
# <a name="srv_setutype-extended-stored-procedure-api"></a>srv_setutype（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 为行中的列设置用户定义数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_setutype (  
SRV_PROC *  
srvproc  
,  
int   
column  
,   
DBINT  
user_type   
);  
  
```  
  
## <a name="arguments"></a>参数  
 srvproc**  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *该列*  
 指示要设置的列。 列的编号从 1 开始。  
  
 *user_type*  
 指定用户定义数据类型的代码。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。 如果相应列不存在，则返回 FAIL。  
  
## <a name="remarks"></a>备注  
 列具有两种数据类型：其实际数据类型及其用户定义数据类型。 用户定义数据类型由[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于存储列的实际用户定义数据类型（如果有）和列说明信息（如为空性和可更新性）。  
  
 在使用 srv_describe 定义列后，并且在发送最后一行前，随时都可以调用 srv_setutype 函数**********。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [srv_describe（扩展存储过程 API）](srv-describe-extended-stored-procedure-api.md)  
  
  
