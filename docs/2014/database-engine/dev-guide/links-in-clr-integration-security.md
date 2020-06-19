---
title: CLR 集成安全性中的链接 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- table-access links [CLR integration]
- security [CLR integration]
- invocation links [CLR integration]
- gated links [CLR integration]
ms.assetid: 168efd01-d12e-4bdf-a1b3-0b5c76474eaf
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 50f7a685a57bf07b812aefc2bd5406210b86054c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933504"
---
# <a name="links-in-clr-integration-security"></a>CLR 集成安全性中的链接
  本节介绍使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或某种托管语言的用户代码片段怎样才能在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中相互调用。 对象之间的这些关系称为链接。  
  
## <a name="invocation-links"></a>调用链接  
 调用链接对应于代码调用，该调用要么来自调用对象的用户（比如调用存储过程的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批），要么来自公共语言运行库 (CLR) 存储过程或函数。 调用链接将导致检查对被调用方的 `EXECUTE` 权限。  
  
## <a name="table-access-links"></a>表访问链接  
 表访问链接对应于在表、视图或表值函数中检索或修改值。 它们类似于调用链接，但它们在 SELECT、INSERT、UPDATE 和 DELETE 权限方面有较粗粒度的访问控制权。  
  
## <a name="gated-links"></a>封闭链接  
 门链接意味着，在执行期间，一旦已建立对象关系，则不跨越该对象关系检查权限。 如果两个对象（例如，对象**x**和对象**y**）之间有一个封闭链接，则仅在创建对象**x**时检查对象**y**上和从对象**y**访问的其他对象的权限。 在创建对象**x**时，将根据 `REFERENCE` **x**的所有者对**y**检查权限。 执行时（例如，当某人调用 object **x**）时，不会针对其静态引用的**y**或其他对象检查权限。 执行时，将对照对象**x**本身来检查适当的权限。  
  
 门链接始终与两个对象之间的元数据依赖性配合使用。 该元数据依赖性是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录中建立的关系，它使得只要另一个对象依赖于某个对象则无法删除该对象。  
  
 如果向很多依赖性对象授权是不合适或不可管理的，则需要使用门链接。 在定义到 CLR 程序集（例如，CLR 过程、触发器、函数、类型和聚合）的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 入口点的对象与其中定义它们的程序集之间引入了门链接。 对应这些对象的门安全性暗含如下法则：为了调用在 CLR 程序集中定义的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 入口点，调用方只需对该 [!INCLUDE[tsql](../../includes/tsql-md.md)] 入口点有合适的权限。 调用方不必对该程序集或它静态引用的任何其他程序集拥有权限。 在创建 [!INCLUDE[tsql](../../includes/tsql-md.md)] 入口点时将检查程序集上的权限。  
  
## <a name="sql-server-authorization-based-security"></a>SQL Server 基于授权的安全性  
 下面是对调用基于 CLR 的数据库对象和这些对象之间的调用进行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全检查所基于的基本规则；前三个规则定义了将检查哪些权限和根据哪个对象进行检查；第四个规则定义了根据哪个执行上下文来检查权限。  
  
1.  所有调用都需要 `EXECUTE` 权限，除非调用发生在相同对象内；这意味着相同程序集内的调用不需要进行任何权限检查。 权限检查在执行时进行。  
  
2.  创建调用对象时，门链接需要拥有对被调用方的 `REFERENCE` 权限。 创建对象时，系统将检查调用对象的所有者是否有此权限。  
  
3.  表访问链接需要拥有对被访问的表或视图的相应的 `SELECT`、`INSERT`、`UPDATE` 或 `DELETE` 权限。  
  
4.  系统根据当前执行上下文检查此权限。 可以用不同于调用方的执行上下文创建过程和函数。 程序集始终以根据它定义的过程、函数或触发器的执行上下文来创建。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
