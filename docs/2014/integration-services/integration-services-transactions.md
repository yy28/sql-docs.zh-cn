---
title: Integration Services 事务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0359ca10e7279f4a80bec082a8e049f4641c9b2
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389055"
---
# <a name="integration-services-transactions"></a>Integration Services 事务
  包使用事务将任务执行的数据库操作绑定到原子单元中，这样做可以维护数据的完整性。 所有 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 容器类型（包、For 循环、Foreach 循环和序列容器以及封装每个任务的任务宿主）都可以配置为使用事务。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供用于配置事务的三个选项：**NotSupported**，**支持**，和**所需**。  
  
-   **Required** 指示该容器启动一个事务，除非已经存在由其父容器启动的事务。 如果事务已经存在，容器将联接该事务。 例如，如果没有配置为支持事务的包包括一个使用 **Required** 选项的序列容器，则该序列容器会启动其自己的事务。 如果包已经配置为使用 **Required** 选项，则序列容器将联接包事务。  
  
-   **Supported** 指示容器不启动事务，但将联接由其父容器启动的任何事务。 例如，如果具有四个执行 SQL 任务的包启动了一个事务，而且所有这四个任务都使用 **Supported** 选项，则在其中任何一个任务失败时都会回滚执行 SQL 任务所执行的数据库更新。 如果包没有启动事务，则四个执行 SQL 任务将不绑定到该事务，而且除了回滚失败的任务所执行的更新外，不回滚任何其他数据库更新。  
  
-   **NotSupported** 指示容器不启动事务，也不联接现有事务。 由父容器启动的事务不影响已经配置为不支持事务的子容器。 例如，如果包配置为启动事务，而包中的 For 循环容器使用 **NotSupported** 选项，则在 For 循环中的任务失败时不回滚任何任务。  
  
 通过设置容器的 TransactionOption 属性，你可以配置事务。 您可以使用 **中的** “属性” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]窗口设置此属性，也可以通过编程方式设置此属性。  
  
> [!NOTE]  
>  `TransactionOption` 属性影响是否应用由容器请求的 `IsolationLevel` 属性的值。 有关详细信息，请参阅的说明`IsolationLevel`主题中的属性[设置包属性](set-package-properties.md)。  
  
### <a name="to-configure-a-package-to-use-transactions"></a>将包配置为使用事务  
  
-   [将包配置为使用事务](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
## <a name="external-resources"></a>外部资源  
  
-   www.mssqltips.com 上的博客项 [How to Use Transactions in SQL Server Integration Services SSIS](https://go.microsoft.com/fwlink/?LinkId=157783)（如何在 SQL Server Integration Services SSIS 中使用事务）  
  
## <a name="see-also"></a>请参阅  
 [继承的事务](../../2014/integration-services/inherited-transactions.md)   
 [多个事务](../../2014/integration-services/multiple-transactions.md)  
  
  
