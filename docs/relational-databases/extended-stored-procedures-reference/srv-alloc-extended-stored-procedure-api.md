---
title: srv_alloc（扩展存储过程 API）| Microsoft Docs
description: 了解扩展存储过程 API 中的 srv_alloc 以及它如何动态分配内存。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_alloc
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_alloc
ms.assetid: 91505c59-a273-452f-b71d-5e8205c21863
author: rothja
ms.author: jroth
ms.openlocfilehash: b2caa2f1a3959a723854c94a474a20e966f54fb5
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332377"
---
# <a name="srv_alloc-extended-stored-procedure-api"></a>srv_alloc（扩展存储过程 API）
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 动态分配内存。  
  
## <a name="syntax"></a>语法  
  
```  
  
void * srv_alloc ( DBINT  
size  
);  
```  
  
## <a name="arguments"></a>参数  
 *大小*  
 指定要分配的字节数。  
  
## <a name="returns"></a>返回  
 指向新分配的空间的指针。 如果无法分配 size 字节，则返回 Null 指针**。  
  
## <a name="remarks"></a>备注  
 srv_alloc 函数等效于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows API GlobalAlloc 函数********。 可以在扩展存储过程 API 应用程序中使用普通 Windows API C 运行时内存管理函数。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
