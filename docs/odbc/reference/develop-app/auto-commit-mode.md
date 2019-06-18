---
title: 自动提交模式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 491fb8db9e37cfb3bfa07881958fe7828e6bb911
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048421"
---
# <a name="auto-commit-mode"></a>自动提交模式
*在自动提交模式下，* 每个数据库操作是在执行时已提交的事务。 此模式适合用于包含单个 SQL 语句的许多实际的事务。 不需要分隔，或者指定的这些事务完成。 在数据库中不支持事务的情况下，自动提交模式是唯一支持的模式。 在此类数据库语句仅在提交后可以执行它们并没有方法回滚它们;它们因此始终处于自动提交模式。  
  
 如果遵循基础 DBMS 不支持自动提交模式下事务，该驱动程序可以模拟它们通过手动提交每个 SQL 语句，因为它执行。  
  
 如果在自动提交模式下执行一批 SQL 语句，则它是数据源特定的语句批处理中提交时。 它们可以是已提交会在执行时或作为一个整体后执行整个批处理。 某些数据源可能支持这两个这些行为，并且可能会提供一种方法选择一个或其他人。 具体而言，如果批处理过程中发生错误，则数据源特定于已执行语句是提交还是回滚。 因此，使用批次，且需要它们来提交或回滚作为一个整体的可互操作应用程序应仅在手动提交模式下执行批处理。
