---
description: 扩展存储过程的工作方式
title: 扩展存储过程的工作方式 |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
ms.openlocfilehash: 49c5f3491d93ee71a0ce118a5f4ba387da770f1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460811"
---
# <a name="how-extended-stored-procedures-work"></a>扩展存储过程的工作方式

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 请改用 CLR 集成。  
  
 扩展存储过程的工作流程是：  
  
1.  当客户端执行扩展存储过程时，请求将以表格格式数据流 (TDS) 或简单对象访问协议 (SOAP) 格式从客户端应用程序传输到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 搜索与扩展存储过程关联的 DLL 并加载此 DLL（如果尚未加载）。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 调用请求的扩展存储过程（在 DLL 内部作为函数实现）。  
  
4.  扩展存储过程通过扩展存储过程 API 传递结果集，并将参数返回给服务器。  

