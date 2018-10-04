---
title: 应用程序域和 CLR 集成安全性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- application domains [CLR integration]
ms.assetid: 54ee904e-e21a-4ee7-b4ad-a6f6f71bd473
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34814ab19f96ff7e6232638ef4446b05b5b41ba3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102338"
---
# <a name="application-domains-and-clr-integration-security"></a>应用程序域和 CLR 集成安全性
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将加载在相同应用程序域中属于相同所有者的程序集。 由于一组程序集运行于相同应用程序域中，因此程序集能够使用 the.NET Framework 反射应用程序编程接口或其他手段在执行时彼此发现对方，并且可以用后期绑定的方式调用它们。 由于这样的调用是针对属于相同所有者的程序集发生的，因此不会检查这些调用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 权限。 之所以设计程序集在应用程序域中的放置方案，主要是为了实现可伸缩性、安全性和隔离性目标，并且有可能在未来的版本中进行更改。 因此，不应当依赖于通过后期绑定机制在相同应用程序域中查找程序集。  
  
## <a name="see-also"></a>请参阅  
 [CLR 集成安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
