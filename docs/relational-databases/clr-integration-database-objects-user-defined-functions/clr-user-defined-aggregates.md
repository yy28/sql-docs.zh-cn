---
title: CLR 用户定义聚合 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e654e1e14aa09e5414a100e6d06c64eba93dab7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68009798"
---
# <a name="clr-user-defined-aggregates"></a>CLR 用户定义聚合
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  聚合函数对一组值进行计算，返回单个值。 传统上[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，只支持对一组输入标量值执行的内置聚合函数（如**SUM**或**MAX**），并从该集生成单个聚合值。 通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 公共语言运行时 (CLR) 的集成，现在开发人员能够利用托管代码创建自定义聚合函数，并且使这些函数可供 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他托管代码访问。  
  
 下表列出了本节的主题。  
  
 [CLR 用户定义聚合的要求](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 概述用于实现 CLR 用户定义聚合函数的要求。  
  
 [调用 CLR 用户定义聚合函数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 说明如何调用用户定义聚合。  
  
  
