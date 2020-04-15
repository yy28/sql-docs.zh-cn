---
title: 自动提交模式 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f19053eec7a48eba7a51425b01744f3acd10015
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285107"
---
# <a name="auto-commit-mode"></a>自动提交模式
*在自动提交模式下，* 每个数据库操作都是执行时提交的事务。 此模式适用于由单个 SQL 语句组成的许多实际事务。 没有必要对这些事务的完成进行分隔或指定。 在没有事务支持的数据库中，自动提交模式是唯一支持的模式。 在此类数据库中，语句在执行时被提交，无法回滚它们;因此，它们始终处于自动提交模式。  
  
 如果基础 DBMS 不支持自动提交模式事务，则驱动程序可以通过在执行每个 SQL 语句时手动提交来模拟它们。  
  
 如果在自动提交模式下执行一批 SQL 语句，则当提交批处理中的语句时，它是特定于数据源的。 它们可以在执行时提交，也可以在整个批处理执行后作为一个整体提交。 某些数据源可能支持这两种行为，并可能提供一种选择其中一种或另一种行为的方法。 特别是，如果批处理中间发生错误，则是特定于数据源的语句，无论是已提交还是回滚已执行的语句。 因此，使用批处理并要求它们作为整体提交或回滚的可互操作应用程序应仅在手动提交模式下执行批处理。
