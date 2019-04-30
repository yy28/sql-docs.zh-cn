---
title: srv_got_attention（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_got_attention
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1b2b13668c9402d947937b4cc7aeb581c253d6a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127290"
---
# <a name="srvgotattention-extended-stored-procedure-api"></a>srv_got_attention（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 请检查是否需要中止当前连接或任务以及在连接已终止或批已中止时是否返回 TRUE。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL srv_got_attention  
(SRV_PROC *  
srvproc  
);  
  
```  
  
#### <a name="parameters"></a>Parameters  
 srvproc  
 标识数据库连接的指针。  
  
## <a name="return-value"></a>返回值  
 如果连接已终止或者批已中止，则为 TRUE。 如果连接或批处于活动状态，则为 FALSE。  
  
## <a name="remarks"></a>备注  
 长时间运行的扩展存储过程应通过定期调用 srv_got_attention 来检查服务器的关注情况，这样使过程可以在连接终止或批处理中止时终止自身。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
  
