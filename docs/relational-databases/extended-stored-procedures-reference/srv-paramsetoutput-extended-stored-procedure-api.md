---
title: srv_paramsetoutput（扩展存储过程 API）
description: 了解扩展存储过程 API 中 srv_paramsetoutput 如何设置返回参数的值。
ms.custom: seo-dt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramsetoutput
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
author: rothja
ms.author: jroth
ms.openlocfilehash: 3e406d8a9f2b9bc6b2f03239dee435364f481af9
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248381"
---
# <a name="srv_paramsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput（扩展存储过程 API）
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 设置返回参数的值。 此函数取代了 srv_paramset 函数****。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_paramsetoutput (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbData  
,  
ULONG   
cbLen  
,  
BOOL  
fNull   
);  
```  
  
## <a name="arguments"></a>参数  
 srvproc**  
 客户端连接的句柄。  
  
 *n*  
 要设置的参数的序号。 第一个参数是 1。  
  
 pbData**  
 指向要作为存储返回参数发送回客户端的数据值的指针。  
  
 cbLen**  
 要返回的数据的实际长度。 如果参数的数据类型指定了常量长度值且不允许 Null 值（例如 srvbit 或 srvint1），则将会忽略 cbLen******。 如果 fNull 为 FALSE，值为 0 则表示长度为零的数据**。  
  
 fNull**  
 指示返回参数的值是否为 NULL 的标志。 如果应将该参数设置为 NULL，请将此标志设置为 TRUE。 默认值是 FALSE。 如果 fNull 设置为 TRUE，cbLen 应设置为 0，否则该函数将失败****。  
  
## <a name="returns"></a>返回值  
 如果成功设置了参数信息，则返回 SUCCEED，否则返回 FAIL。 以下情况下返回 FAIL：  
  
-   该参数不是返回参数，或者  
  
-   cbLen 参数无效**。  
  
## <a name="remarks"></a>备注  
 **安全说明** 应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，应对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
