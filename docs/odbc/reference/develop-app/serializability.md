---
title: 可序列化性 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6e912ec51bc0b7c77d73aae1b473dee9242b3f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913622"
---
# <a name="serializability"></a>可序列化性
理想情况下，事务应*可序列化*。 事务可认为是如果同时运行事务的结果是否相同按顺序运行它们的结果，可序列化-一个接一个，即。 它并不重要的事务，则首先执行，仅，结果不会反映任何事务的混合。  
  
 例如，假设事务 A 将数据值与 2 相乘并事务 B 将 1 添加到数据值。 现在，假设有两个数据值： 0 和 10。 如果这些事务运行一个接一个，新值将是 1 和 21 如果首先，运行事务 A 或 2 和 22，如果先运行事务 B。 但是，如果在其中运行两个事务的顺序是不同的每个值？ 如果一个运行的第一个值在第一个事务和事务 B 第一个上运行的第二个值，则新值将是 1 和 22。 如果此顺序被反转，则新值将是 2 和 21。 这些事务是可序列化 22 如果 1、 21 和 2，是唯一的可能结果。 这些事务是不可序列化的如果 1、 22 或 2、 21 是可能的结果。  
  
 因此为何需要的可序列化性？ 换而言之，为什么很重要，它显示该一个事务完成之前的下一个事务启动？ 请考虑以下问题。 一位销售人员正在分配器发出的帐单的同时进入订单。 假设推销商从 X 公司输入一个订单，但不提交它;推销商仍在与客户支持代表从公司 X 交谈。Clerk 请求的所有未结订单的列表和发现公司 X 的顺序并将它们发送帐单。 现在从 X 公司代表决定他们想要更改其顺序，因此在提交事务之前的推销商更改它。 公司 X 获取正确的帐单。  
  
 如果推销商的和分配器的事务可序列化，将永远不会发生此问题。 推销商的事务将所花费的时间启动的分配器的事务，出正确的帐单，已在此情况下发送 clerk 或之前推销商的事务启动，在这种情况下，将已完成的分配器的事务分配器将不发送帐单给公司 X 根本。
