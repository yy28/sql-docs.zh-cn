---
title: Serializability |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0557e011578d313765614c05a2a9cf1b975bbc08
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304158"
---
# <a name="serializability"></a>可序列化性
理想情况下，事务应该是可*序列化*的。 如果运行中的事务的结果与按顺序运行事务的结果相同（即一个接一个），则认为该事务是可序列化的。 首先执行的事务并不重要，只是结果并不反映任何事务的混合。  
  
 例如，假设 transaction A 将数据值乘以2，事务 B 会将1添加到数据值。 现在假设有两个数据值：0和10。 如果这些事务逐个运行，则新值将为1，21如果首先运行事务 A，则新值为1，如果首先运行事务 B，则新值为2和22。 但是，如果两个事务的运行顺序不同于每个值，该怎么办呢？ 如果在第一个值上首先运行事务 A，并且首先对第二个值运行事务 B，则新值为1和22。 如果反转此顺序，则新值为2和21。 如果1、21和2，则事务是可序列化的。 如果1、22或2，则可能会导致事务无法序列化。  
  
 那么为什么需要 serializability 呢？ 换句话说，为什么在下一个事务启动前，一个事务已完成，这一点很重要？ 请考虑以下问题。 销售员在发送帐单的同时，输入了订单。 假设销售商输入来自公司 X 的订单，但不提交该订单;销售商仍与公司 X 的代表交谈。该职员请求一个列表，其中列出了所有打开的订单，并发现公司 X 的订单并向其发送了帐单。 现在，公司 X 的代表决定要更改其订单，因此，销售人员在提交交易之前将其更改。 公司 X 获取的帐单不正确。  
  
 如果销售员和人员的事务是可序列化的，则此问题永远不会发生。 推销员的交易将在该职员的事务开始之前完成，在这种情况下，该职员将发送正确的帐单，或该职员的交易将在销售人员的交易开始之前完成，在这种情况下，该职员根本不会向公司 X 发送帐单。
