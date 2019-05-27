---
title: 多个事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], multiple
- multiple transactions
ms.assetid: c3664a94-be89-40c0-a3a0-84b74a7fedbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da0f932acb2ab97204aeb27c9e077c7fae154987
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057401"
---
# <a name="multiple-transactions"></a>多个事务
  包可以在一个 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包中包含不相关的事务。 无论任何时候，位于嵌套容器层次结构中间的容器都不支持事务，位于层次结构中其他位置的容器如果配置为支持事务，则它们将启动单独的事务。 事务按照从嵌套容器层次结构中最里面的任务到包这个顺序来提交或回滚。 但是，在内部事务提交后，如果外部事务中止，已提交的事务不会回滚。  
  
## <a name="illustration-of-multiple-transactions"></a>多个事务的说明  
 例如，某个包包含一个序列容器，该序列容器中又存储有两个 Foreach 循环容器，而后面这两个容器中又分别包含两个执行 SQL 任务。 序列容器支持事务，而 Foreach 循环容器则不支持事务，但执行 SQL 任务支持。 在此示例中，每个执行 SQL 任务都将启动自己的事务，如果序列任务上的事务被中止，则执行 SQL 任务将不会回滚。  
  
 序列容器、Foreach 循环容器和执行 SQL 任务的 TransactionOption 属性按照如下方式进行设置：  
  
-   序列容器的 TransactionOption 属性设置为 **Required**。  
  
-   Foreach 循环容器的 TransactionOption 属性设置为 **NotSupported**。  
  
-   执行 SQL 任务的 TransactionOption 属性设置为 **Required**。  
  
 下面的关系图显示了包中的五个不相关的事务。 一个事务是由序列容器启动的，其余四个事务是由执行 SQL 任务启动的。  
  
 ![多个事务的实现](media/mw-dts-trans2.gif "Implementation of multiple transactions")  
  
## <a name="related-tasks"></a>Related Tasks  
 [将包配置为使用事务](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
