---
title: srv_got_attention（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_got_attention
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
author: rothja
ms.author: jroth
ms.openlocfilehash: f30e546a5cd45d9c89923ab9e96670127491f1ff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756746"
---
# <a name="srv_got_attention-extended-stored-procedure-api"></a>srv_got_attention（扩展存储过程 API）
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 请检查是否需要中止当前连接或任务以及在连接已终止或批已中止时是否返回 TRUE。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL srv_got_attention (SRV_PROC *   
srvproc  
);  
```  
  
#### <a name="parameters"></a>参数  
 srvproc**  
 标识数据库连接的指针。  
  
## <a name="return-value"></a>返回值  
 如果连接已终止或者批已中止，则为 TRUE。 如果连接或批处于活动状态，则为 FALSE。  
  
## <a name="remarks"></a>备注  
 长时间运行的扩展存储过程应通过定期调用 srv_got_attention 来检查服务器的关注情况，这样使过程可以在连接终止或批处理中止时终止自身****。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
