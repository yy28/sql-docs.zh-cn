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
ms.openlocfilehash: a8a02d58309f123e6cc8b29d41188ba5bebb26f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909892"
---
# <a name="auto-commit-mode"></a>自动提交模式
*在自动提交模式下，* 每个数据库操作都是在执行时提交的事务。 此模式适用于由单个 SQL 语句组成的多个实际事务。 不需要分隔或指定完成这些事务。 在不支持事务的数据库中，自动提交模式是唯一受支持的模式。 在这种情况下，在执行语句时，将提交语句，而且无法回滚语句;因此，它们始终处于自动提交模式。  
  
 如果基础 DBMS 不支持自动提交模式事务，则驱动程序可以通过在执行每个 SQL 语句时手动提交这些事务来模拟它们。  
  
 如果一批 SQL 语句以自动提交模式执行，则在提交批处理中的语句时，该语句是特定于数据源的。 在执行整个批处理后，可以提交它们，或将其作为一个整体执行。 某些数据源可能同时支持这两种行为，并可提供一种方法来选择其中一个。 具体而言，如果在批处理中间发生错误，则无论是提交还是回滚已执行的语句，它都是特定于数据源的。 因此，使用批处理并要求它们作为整体进行提交或回滚的可互操作应用程序只应在手动提交模式下执行批处理。
