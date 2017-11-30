---
title: "srv_paraminfo（扩展存储过程 API）| Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_paraminfo
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_paraminfo
ms.assetid: ee2afd4e-0d91-462b-9403-98d481546330
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0cacc7a1186ece828183d26223677e0f10ffa25
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="srvparaminfo-extended-stored-procedure-api"></a>srv_paraminfo（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 返回有关参数的信息。 此函数取代了以下函数：[srv_paramtype](../../relational-databases/extended-stored-procedures-reference/srv-paramtype-extended-stored-procedure-api.md)、[srv_paramlen](../../relational-databases/extended-stored-procedures-reference/srv-paramlen-extended-stored-procedure-api.md)、[srv_parammaxlen](../../relational-databases/extended-stored-procedures-reference/srv-parammaxlen-extended-stored-procedure-api.md) 和 [srv_paramdata](../../relational-databases/extended-stored-procedures-reference/srv-paramdata-extended-stored-procedure-api.md)。 srv_paraminfo 支持[数据类型](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)中的数据类型和长度为零的数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_paraminfo (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbType  
,  
ULONG *  
pcbMaxLen  
,  
ULONG *  
pcbActualLen  
,  
BYTE *  
pbData  
,  
BOOL *  
pfNull  
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 客户端连接的句柄。  
  
 *n*  
 要设置的参数的序号。 第一个参数是 1。  
  
 pbType  
 参数的数据类型。  
  
 pcbMaxLen  
 指向参数的最大长度的指针。  
  
 pcbActualLen  
 指向参数的实际长度的指针。 如果 *pfNull 设置为 FALSE，值为 0 (\*pcbActualLen == 0) 表示长度为零的数据。  
  
 pbData  
 指向参数数据的缓冲区的指针。 如果 pbData 不为 NULL，扩展存储过程 API 将 \*pcbActualLen 字节的数据写入 \*pbData。 如果 pbData 为 NULL，不会有任何数据写入 \*pbData，但函数返回 \*pbType、\*pcbMaxLen、\*pcbActualLen 和 *pfNull。 此缓冲区的内存必须由应用程序管理。  
  
 pfNull  
 指向 Null 标志的指针。如果参数的值为 NULL， *pfNull 设置为 TRUE。  
  
## <a name="returns"></a>返回  
 如果成功获取参数信息，则返回 SUCCEED，否则返回 FAIL。 如果没有当前远程存储过程并且没有第 n 个远程存储过程参数，则返回 FAIL。  
  
## <a name="remarks"></a>注释  
 **安全说明** 应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，应对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [扩展存储过程程序员参考](../../relational-databases/extended-stored-procedures-reference/database-engine-extended-stored-procedures-reference.md)  
  
  
