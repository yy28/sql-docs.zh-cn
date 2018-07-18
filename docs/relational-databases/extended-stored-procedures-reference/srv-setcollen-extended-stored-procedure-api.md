---
title: srv_setcollen（扩展存储过程 API）| Microsoft Docs
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
- srv_setcollen
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setcollen
ms.assetid: 3c60f1c3-4562-463a-a259-12df172788bd
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6e647374b9c313be9b19aa81325fa4fb85bd8ffc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32935122"
---
# <a name="srvsetcollen-extended-stored-procedure-api"></a>srv_setcollen（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 指定长度可变的列或允许 NULL 值的列的当前数据长度（以字节为单位）。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_setcollen (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *column*  
 指示指定其数据长度的列的编号。 列的编号从 1 开始。  
  
 len  
 指示列数据的长度（以字节为单位）。 长度为 0 表示列数据值为 Null。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>Remarks  
 必须首先使用 srv_describe 定义行的每个列。 列数据长度通过对 srv_describe 或 srv_setcollen 的最后一次调用进行设置。 如果某一行长度可变的数据（以 Null 值结束的数据）发生更改，必须使用 srv_setcollen 将该数据设置为新的长度，然后才能调用 srv_sendrow。 对于允许 Null 值的列，必须已调用 srv_describe，并将 desttype 设置为允许 Null 值的数据类型（如 SRVINTN），NULL 数据的指定方法是：调用 srv_setcollen 并将 len 设置为 0。 不能使用扩展存储过程 API 指定长度为零的数据。  
  
 请注意，当列数据类型的长度可变时，则不检查 len。 如果调用固定长度的列，该函数则返回 FAIL。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [srv_describe（扩展存储过程 API）](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
