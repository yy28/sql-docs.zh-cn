---
title: CLR 用户定义聚合 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
ms.openlocfilehash: 23e17d38fdd38b398519457a64d0fc61115ad54a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32918012"
---
# <a name="clr-user-defined-aggregates"></a>CLR 用户定义聚合
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  聚合函数对一组值执行计算，并返回单个值。 传统上， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有支持仅内置聚合函数，如**总和**或**最大**的一组输入标量值进行操作，并且生成单个聚合从该组的值。 通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 公共语言运行时 (CLR) 的集成，现在开发人员能够利用托管代码创建自定义聚合函数，并且使这些函数可供 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他托管代码访问。  
  
 下表列出了本节的主题。  
  
 [CLR 用户定义聚合的要求](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 概述用于实现 CLR 用户定义聚合函数的要求。  
  
 [调用 CLR 用户定义聚合函数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 说明如何调用用户定义聚合。  
  
  
