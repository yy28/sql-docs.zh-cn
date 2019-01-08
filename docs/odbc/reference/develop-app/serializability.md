---
title: 可序列化性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7972fb72607edca8c1599c2d028b073c184642
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518292"
---
# <a name="serializability"></a>可序列化性
理想情况下，事务应*可序列化*。 事务被称为可串行-运行它们的结果作为的同时运行的事务的结果是相同的情况下序列化一个接一个即。 它并不重要的事务，则首先执行，仅的结果不会反映任何混合的事务。  
  
 例如，假设事务 A 将数据值乘以 2 并事务 B 将 1 添加到数据值。 现在假设有两个数据值：0 到 10。 如果这些事务运行一个接一个，新值将是 1、 21 如果首先，运行事务 A 或 2 和 22，如果事务 B 运行第一个。 但是，如果两个事务的运行顺序是不同的每个值？ 如果一个运行的第一个值中第一个事务，事务 B 运行第一个在第二个值，则新值是 1 和 22。 如果此顺序颠倒，新值为 2 和 21。 这些事务是可序列化 22 1、 21 和 2，如果是唯一可能的结果。 这些事务是不如果 1、 22 或 2、 21，可序列化是可能的结果。  
  
 那么为什么是可序列化性需要呢？ 换而言之，为什么很重要的那样显示，一个事务完成之前启动的下一个事务？ 请考虑以下问题。 一位销售人员一个分配器发送出的帐单的同时输入订单。 假设在推销员从 X 公司进入订单，但不会提交它;商仍与代表通话从 X 公司。分配器请求的所有打开的订单列表和发现 X 公司的顺序并将其发送一份帐单。 现在，客户支持代表从 X 公司决定他们想要更改它们的顺序，因此商提交事务之前更改它。 X 公司获取不正确的帐单。  
  
 如果可序列化的商的和分配器的事务，将永远不会发生此问题。 商的事务将所花费的时间启动 clerk 的事务，出正确的帐单，已在此情况下发送的分配器或 clerk 的事务将所花费的时间在推销员事务启动，在这种情况下分配器会有根本不发送一份帐单到 X 公司。
