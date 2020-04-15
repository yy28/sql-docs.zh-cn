---
title: 可序列化 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304158"
---
# <a name="serializability"></a>可序列化性
理想情况下，事务应该是*可序列化的*。 如果同时运行事务的结果与串行运行事务的结果相同（即一个接一个）时，事务就表示可序列化。 首先执行哪个事务并不重要，只是结果不反映事务的任何混合。  
  
 例如，假设事务 A 将数据值乘以 2，事务 B 将 1 添加到数据值。 现在假设有两个数据值：0 和 10。 如果这些事务一个接一个运行，则如果事务 A 先运行，则新值为 1 和 21;如果事务 B 先运行，则为 2 和 22。 但是，如果两个事务的运行顺序因每个值而异，该怎么办？ 如果事务 A 先在第一个值上运行，而事务 B 在第二个值上首先运行，则新值为 1 和 22。 如果反转此顺序，则新值为 2 和 21。 如果唯一可能的结果为 1、21 和 2、22，则事务是可序列化的。 如果可能是 1、22 或 2、21，则事务不可序列化。  
  
 那么，为什么序列化是可取的呢？ 换句话说，为什么在下一个事务开始之前，一个事务似乎完成很重要？ 请考虑以下问题。 一个推销员正在输入订单，同时一个职员正在发单。 假设销售员从 X 公司输入订单，但不提交订单;售货员还在和X公司的代表谈话。店员请求所有已结订单的列表，并发现公司 X 的订单并发送给他们帐单。 现在，公司 X 的代表决定要更改订单，因此销售员在提交交易之前更改了订单。 公司 X 收到不正确的帐单。  
  
 如果销售员和职员的交易是可连载的，那么这个问题就不会发生。 要么销售员的交易在店员的交易开始之前就完成，在这种情况下，职员会寄出正确的帐单，要么职员的交易在销售员的交易开始之前完成，在这种情况下，职员根本不会向 X 公司发送帐单。
