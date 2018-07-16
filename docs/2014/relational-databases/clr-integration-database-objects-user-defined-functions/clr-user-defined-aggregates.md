---
title: CLR 用户定义聚合 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cbc2929f11b37d58745af6ca5b25bf34221b9478
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37352469"
---
# <a name="clr-user-defined-aggregates"></a>CLR 用户定义聚合
  聚合函数对一组值执行计算，并返回单个值。 一直以来， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持仅内置聚合函数，如`SUM`或`MAX`的一组输入标量值进行操作，并且从该组值生成单个聚合值。 通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 公共语言运行时 (CLR) 的集成，现在开发人员能够利用托管代码创建自定义聚合函数，并且使这些函数可供 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他托管代码访问。  
  
 下表列出了本节的主题。  
  
 [CLR 用户定义聚合的要求](clr-user-defined-aggregates-requirements.md)  
 概述用于实现 CLR 用户定义聚合函数的要求。  
  
 [调用 CLR 用户定义聚合函数](clr-user-defined-aggregate-invoking-functions.md)  
 说明如何调用用户定义聚合。  
  
  
