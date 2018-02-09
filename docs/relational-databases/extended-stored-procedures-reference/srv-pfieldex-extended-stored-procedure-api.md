---
title: "srv_pfieldex（扩展存储过程 API）| Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- srv_pfieldex
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70f36511846d7435cc940ea65f871c462130958d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="srvpfieldex-extended-stored-procedure-api"></a>srv_pfieldex（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 返回一个指针，指向包含请求的 SRV_PROC 字段的数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
void *srv_pfieldex(SRV_PROC *   
srvproc  
, int   
field  
, int *   
len  
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 field  
 指定要返回的 srvproc 字段。  
  
|字段|Description|返回类型|  
|-----------|-----------------|------------------|  
|SRV_MSGLCID|当前会话消息 LCID。|ULONG*|  
|SRV_INSTANCENAME|实例名称（如果已命名）；否则返回 NULL。|WCHAR*|  
  
 len  
 指向一个 int 变量的指针，该变量包含所返回的 field 值的长度（以字节为单位）。 如果 len 为 NULL，则不返回长度。 返回 NULL 时，*len 设置为 0。  
  
## <a name="returns"></a>返回  
 一个指针，指向其类型取决于 field 的数据。 len 为 NULL 或 srvproc 为 NULL 时，则返回 NULL。 如果 field 未知，则返回 NULL。 返回 NULL 时，*len 设置为 0。  
  
> [!IMPORTANT]  
>  从服务器返回的缓冲区应为只读的。 否则，可能损坏服务器状态。  
  
## <a name="remarks"></a>注释  
 **安全说明** 应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，应对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
  
