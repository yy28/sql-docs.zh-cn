---
title: 继承的事务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], inherited
- child packages
- inherited transactions [Integration Services]
ms.assetid: 90db5564-d41e-4cfe-8c9e-4e68d41eff1c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3f3555125032b5409f53b802990df0e5da04954f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058437"
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
  
-   对于包 A 和包 C，**TransactionOption** 设置为 **Required** 。  
  
-   对于包 B 和包 D 以及任务执行包 B、执行包 D 和执行包 F，**TransactionOption** 设置为 **Supported** 。  
  
-   对于包 E 以及任务执行包 C 和执行包 E，**TransactionOption** 设置为 **NotSupported** 。  
  
 ![继承的事务流](media/mw-dts-executepack.gif "Flow of inherited transactions")  
  
 只有包 B、包 D 和包 F 可以从它们的父包继承事务。  
  
 包 B 和包 D 继承包 A 启动的事务。  
  
 包 F 继承包 C 启动的事务。  
  
 包 A 和包 C 控制它们自己的事务。  
  
 包 E 不使用事务。  
  
## <a name="related-tasks"></a>Related Tasks  
 [将包配置为使用事务](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
