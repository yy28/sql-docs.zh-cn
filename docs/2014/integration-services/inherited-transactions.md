---
title: 继承的事务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], inherited
- child packages
- inherited transactions [Integration Services]
ms.assetid: 90db5564-d41e-4cfe-8c9e-4e68d41eff1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8e22375e660e6bcd55c8075edaaba067160279d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058054"
---
# <a name="inherited-transactions"></a>继承的事务
  一个包可以使用执行包任务运行另一个包。 子包也就是执行包任务所运行的包，它可以创建自己的包事务，也可以继承父包事务。  
  
 如果同时满足下面这两个条件，则子包会继承父包事务：  
  
-   该包由执行包任务调用。  
  
-   调用该包的执行包任务同时还联接父包事务。  
  
 子包中的容器和任务无法联接父包事务，除非子包本身联接该事务。  
  
## <a name="illustration-of-package-transactions"></a>包事务的说明  
 在下面的关系图中，三个包都使用事务。 每个包包含多项任务。 为了强调事务的行为，只显示了执行包任务。 包 A 运行包 B 和包 C。而包 B 运行包 D 和包 E，包 C 运行包 F。  
  
 包和任务具有下列事务属性：  
  
-   对于包 A 和 C， **TransactionOption**设置为**Required**  
  
-   对于包 B 和 D 以及任务执行包 B、执行包 D 和执行包 F， **TransactionOption**设置为**支持**。  
  
-   对于包 E， **TransactionOption**设置为**NotSupported** ，在任务执行包 C 和执行包 e 上设置为。  
  
 ![继承的事务流](media/mw-dts-executepack.gif "继承的事务流")  
  
 只有包 B、包 D 和包 F 可以从它们的父包继承事务。  
  
 包 B 和包 D 继承包 A 启动的事务。  
  
 包 F 继承包 C 启动的事务。  
  
 包 A 和包 C 控制它们自己的事务。  
  
 包 E 不使用事务。  
  
## <a name="related-tasks"></a>Related Tasks  
 [将包配置为使用事务](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
