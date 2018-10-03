---
title: 什么是锁定？ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 981b2b5dc1f76d879b18e5569e7fb70dbece1538
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813075"
---
# <a name="what-is-a-lock"></a>什么是锁定？
锁定是 DBMS 将访问限制为多用户环境中的行的过程。 以独占方式锁定行或列，不允许其他用户访问锁定的数据，直到锁被释放。 这可确保两个用户不能同时更新行中的同一列。  
  
 锁会从资源角度来看很高，应仅在需要时保持数据完整性。 在数据库中的数百或数千个用户可能会尝试访问的记录每秒 — 如数据库连接到 Internet，不必要的锁定可能会迅速导致应用程序中的性能下降。  
  
 您可以控制如何在数据源和 ADO 游标库管理通过选择适当的锁定选项的并发。  
  
 设置**LockType**打开之前的属性**记录集**指定打开它时，应使用哪种类型的锁定该提供程序。 要返回的锁定中使用的一种开放类型的属性中读取**记录集**对象。  
  
 提供程序可能不支持所有的锁类型。 如果提供程序无法支持请求**LockType**设置，它将替换为另一种类型的锁定。 若要确定在可用的实际锁定功能**记录集**对象，请使用[支持](../../../ado/reference/ado-api/supports-method.md)方法替换**adUpdate**和**adUpdateBatch**.  
  
 **AdLockPessimistic**如果不支持设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient。** 如果设置不支持的值，不会产生错误;最接近的支持**LockType**将改为使用。  
  
 **LockType**属性为读/写时**记录集**打开时为已关闭，并且是只读的。  
  
 本部分包含以下主题。  
  
-   [锁定类型](../../../ado/guide/data/types-of-locks.md)
