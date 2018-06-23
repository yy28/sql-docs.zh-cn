---
title: 如何扩展存储的过程的工作 |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8b51dc3d5e0401861e188814fd229753428ded9c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018169"
---
# <a name="how-extended-stored-procedures-work"></a>扩展存储过程的工作方式
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 扩展存储过程的工作流程是：  
  
1.  当客户端执行扩展存储的过程时，以表格格式数据流 (TDS) 或客户端应用程序中对简单对象访问协议 (SOAP) 格式传输请求[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 搜索与扩展存储过程关联的 DLL 并加载此 DLL（如果尚未加载）。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 调用请求的扩展存储过程（在 DLL 内部作为函数实现）。  
  
4.  扩展存储过程通过扩展存储过程 API 传递结果集，并将参数返回给服务器。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎扩展存储过程编程](../database-engine-extended-stored-procedure-programming.md)  
  
  