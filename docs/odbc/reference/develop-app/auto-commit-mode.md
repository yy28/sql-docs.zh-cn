---
title: "自动提交模式 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e2127d5b33c5ea4bf2a0c96c5e020322aec39db
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="auto-commit-mode"></a>自动提交模式
*在自动提交模式下，*每个数据库操作是执行时提交的事务。 此模式适合于很多包含单个 SQL 语句的实际事务。 它是不必要分隔或指定这些事务完成。 在数据库中没有事务支持，自动提交模式是唯一支持的模式。 在此类数据库中，语句时，将提交，它们将执行，并且没有无法回滚它们;它们是因此始终在自动提交模式下。  
  
 如果基础的 DBMS 不支持自动提交模式事务，该驱动程序可模拟它们都会在执行手动提交每个 SQL 语句。  
  
 如果在自动提交模式下执行一批 SQL 语句，则它是数据源 – 特定提交批次中的语句时。 它们可以将其提交会在执行时或作为一个整体后执行整个批处理。 某些数据源可能支持这两个这些行为，可以提供一种方法选择一个或其他。 具体而言，如果中间批处理时出错，则数据源 – 特定已执行语句是提交还是回滚。 因此，可互操作应用程序使用批处理，并且需要它们来提交或回滚作为一个整体应仅在手动提交模式下执行批处理。
