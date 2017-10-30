---
title: "什么是锁定？ | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f4975dd903c6d012976f9288b9758e1acab52f1f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="what-is-a-lock"></a>什么是锁定？
锁定是 DBMS 多用户环境中的一行限制访问的过程。 当以独占方式锁定的行或列时，不允许其他用户访问锁定的数据，直至该锁被释放。 这可确保两个用户不能同时更新某一行中的同一列。  
  
 锁可能从资源的角度的开销非常大，应该用于仅在需要时保持数据的完整性。 在其中数百或数千个用户可能会尝试访问的记录每秒数据库-如在数据库连接到 Internet — 不必要的锁定可能会快速导致应用程序中的性能变慢。  
  
 你可以控制如何在数据源和 ADO 游标库管理通过选择适当的锁定选项的并发。  
  
 设置**LockType**属性在打开之前**记录集**以指定在打开时，应使用哪种类型的锁定的提供程序。 读取要返回的锁定中处于打开状态的使用类型的属性**记录集**对象。  
  
 提供程序可能不支持所有的锁类型。 如果提供程序不能支持所请求**LockType**设置，它将替换另一个类型的锁定。 若要确定中可用的实际锁定功能**记录集**对象，请使用[支持](../../../ado/reference/ado-api/supports-method.md)方法替换**adUpdate**和**adUpdateBatch**.  
  
 **AdLockPessimistic**如果不支持设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient。** 如果设置不支持的值，不会产生错误;最近支持**LockType**将改为使用。  
  
 **LockType**属性为读/写时**记录集**打开时为已关闭，并且是只读的。  
  
 本部分包含以下主题。  
  
-   [类型的锁](../../../ado/guide/data/types-of-locks.md)

