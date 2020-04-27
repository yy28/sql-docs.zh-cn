---
title: CLR 用户定义聚合 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 59666e90a47d88762c6fc3bd1fabc0e71ea18f94
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62919583"
---
# <a name="clr-user-defined-aggregates"></a>CLR 用户定义聚合
  聚合函数对一组值执行计算，并返回单个值。 传统上[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，只支持内置聚合函数，例如`SUM`或`MAX`，它对一组输入标量值执行操作，并从该集生成单个聚合值。 通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 公共语言运行时 (CLR) 的集成，现在开发人员能够利用托管代码创建自定义聚合函数，并且使这些函数可供 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他托管代码访问。  
  
 下表列出了本节的主题。  
  
 [CLR 用户定义聚合的要求](clr-user-defined-aggregates-requirements.md)  
 概述用于实现 CLR 用户定义聚合函数的要求。  
  
 [调用 CLR 用户定义聚合函数](clr-user-defined-aggregate-invoking-functions.md)  
 说明如何调用用户定义聚合。  
  
  
