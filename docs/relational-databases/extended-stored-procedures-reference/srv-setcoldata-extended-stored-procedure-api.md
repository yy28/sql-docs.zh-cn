---
title: srv_setcoldata（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setcoldata
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setcoldata
ms.assetid: 2e19205a-25ca-4d4a-916b-d591cf2c892b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cfb3c62f5b0e5f24c84f02e3eba7a9eebb7977fe
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51663186"
---
# <a name="srvsetcoldata-extended-stored-procedure-api"></a>srv_setcoldata（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 指定列的数据的当前地址。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_setcoldata (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
void *  
data   
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *column*  
 指示指定其地址的列的编号。 列的编号从 1 开始。  
  
 data  
 指向列的数据的指针。 在将列数据替换为对 srv_setcoldata 的其他调用或调用 srv_senddone 之前，不能释放为 data 分配的内存。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>Remarks  
 必须首先使用 srv_describe 定义行的每个列。 列数据地址最初使用 srv_describe 进行设置。 如果列数据的地址发生更改，则必须调用 srv_setcoldata 以便指定该数据的新地址，并且必须针对更改后的每个列单独调用 srv_setcoldata。  
  
 使用 srv_setcollen 将列的长度设置为 0 可以表示 Null 数据。 随后将忽略数据地址。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另请参阅  
 [srv_describe（扩展存储过程 API）](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
