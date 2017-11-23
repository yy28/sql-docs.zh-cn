---
title: "如何扩展存储的过程的工作 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 876511657cd65b5ffa683b2df955e403c2c2f1a2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="how-extended-stored-procedures-work"></a>扩展存储过程的工作方式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 扩展存储过程的工作流程是：  
  
1.  当客户端执行扩展存储的过程时，以表格格式数据流 (TDS) 或客户端应用程序中对简单对象访问协议 (SOAP) 格式传输请求[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 搜索与扩展存储过程关联的 DLL 并加载此 DLL（如果尚未加载）。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 调用请求的扩展存储过程（在 DLL 内部作为函数实现）。  
  
4.  扩展存储过程通过扩展存储过程 API 传递结果集，并将参数返回给服务器。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎扩展存储过程编程](../../relational-databases/database-engine-extended-stored-procedure-programming.md)  
  
  
