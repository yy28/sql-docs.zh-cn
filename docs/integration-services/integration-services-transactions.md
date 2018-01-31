---
title: "Integration Services 事务 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 83125af2f2f85c825aae5b594767fa421af2a656
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-transactions"></a>Integration Services 事务
  包使用事务将任务执行的数据库操作绑定到原子单元中，这样做可以维护数据的完整性。 所有 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 容器类型（包、For 循环、Foreach 循环和序列容器以及封装每个任务的任务宿主）都可以配置为使用事务。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供了三个用于配置事务的选项： **NotSupported**、 **Supported**和 **Required**。  
  
-   **Required** 指示该容器启动一个事务，除非已经存在由其父容器启动的事务。 如果事务已经存在，容器将联接该事务。 例如，如果没有配置为支持事务的包包括一个使用 **Required** 选项的序列容器，则该序列容器会启动其自己的事务。 如果包已经配置为使用 **Required** 选项，则序列容器将联接包事务。  
  
-   **Supported** 指示容器不启动事务，但将联接由其父容器启动的任何事务。 例如，如果具有四个执行 SQL 任务的包启动了一个事务，而且所有这四个任务都使用 **Supported** 选项，则在其中任何一个任务失败时都会回滚执行 SQL 任务所执行的数据库更新。 如果包没有启动事务，则四个执行 SQL 任务将不绑定到该事务，而且除了回滚失败的任务所执行的更新外，不回滚任何其他数据库更新。  
  
-   **NotSupported** 指示容器不启动事务，也不联接现有事务。 由父容器启动的事务不影响已经配置为不支持事务的子容器。 例如，如果包配置为启动事务，而包中的 For 循环容器使用 **NotSupported** 选项，则在 For 循环中的任务失败时不回滚任何任务。  
  
 通过设置容器的 TransactionOption 属性，你可以配置事务。 您可以使用 **中的** “属性” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]窗口设置此属性，也可以通过编程方式设置此属性。  
  
> [!NOTE]  
>  **TransactionOption** 属性影响是否应用由容器请求的 **IsolationLevel** 属性的值。 有关详细信息，请参阅 **设置包属性** 主题中 [IsolationLevel](../integration-services/set-package-properties.md)属性的说明。  
  
## <a name="configure-a-package-to-use-transactions"></a>将包配置为使用事务
将包配置为使用事务时，您有两种选择：  
  
-   包仅包含单个事务。 在这种情况下，将由包自身“启动”  此事务，而此包中的各个任务和容器参与此单个事务。  
  
-   包包含多个事务。 在这种情况下，包支持多个事务，但这些事务实际上是由包中的各个任务或容器启动的。  
  
 下面的过程介绍如何配置上述两种选择。  
  
### <a name="configure-a-package-to-use-a-single-transaction"></a>将包配置为使用单个事务  
 在此选择中，程序包自身启动单个事务。 通过将包的 TransactionOption 属性设置为 **必需**可以将包配置为启动此事务。  
  
 接着，在此单个事务中登记特定任务和容器。 若要在事务中登记任务或容器，请将该任务或容器的 TransactionOption 属性设置为 **支持**。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要配置为使用事务的包所在的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  右键单击控制流设计图面背景中的任意位置，然后单击“属性”。  
  
5.  在“属性”窗口中，将 TransactionOption 属性设置为“必需”。  
  
6.  在“控制流”选项卡的设计图面上，右键单击要在事务中注册的任务或容器，再单击“属性”。  
  
7.  在“属性”窗口中，将 TransactionOption 属性设置为“支持”。  
  
    > [!NOTE]  
    >  若要在事务中登记连接，请注册在该事务中使用连接的任务。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
8.  对要在事务中注册的每个任务和容器，请重复步骤 6 和 7。  
  
### <a name="configure-a-package-to-use-multiple-transactions"></a>将包配置为使用多个事务  
 在此选择中，包自身支持但不启动事务。 通过将包的 TransactionOption 属性设置为 **支持**可以将包配置为支持多个事务。  
  
 接着，在包中将所需任务和容器配置为启动或参与事务。 若要将任务或容器配置为启动事务，请将该任务或容器的 TransactionOption 属性设置为 **必需**。   
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要配置为使用事务的包所在的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  右键单击控制流设计图面背景中的任意位置，然后单击“属性”。  
  
5.  在“属性”窗口中，将 TransactionOption 属性设置为“支持”。  
  
    > [!NOTE]  
    >  该包支持事务，但事务是由包中的任务或容器启动的。  
  
6.  在“控制流”选项卡的设计图面上，右键单击要为其启动事务的包中的任务或容器，然后单击“属性”。  
  
7.  在“属性”窗口中，将 TransactionOption 属性设置为“必需”。  
  
8.  如果事务由容器启动，则右键单击要在事务中注册的任务或容器，然后单击“属性”。  
  
9. 在“属性”窗口中，将 TransactionOption 属性设置为“支持”。  
  
    > [!NOTE]  
    >  若要在事务中登记连接，请注册在该事务中使用连接的任务。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
10. 对启动事务的每个任务和容器，请重复步骤 6 到 9。  

## <a name="multiple-transactions-in-a-package"></a>单个包中的多个事务
包可以在一个 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包中包含不相关的事务。 无论任何时候，位于嵌套容器层次结构中间的容器都不支持事务，位于层次结构中其他位置的容器如果配置为支持事务，则它们将启动单独的事务。 事务按照从嵌套容器层次结构中最里面的任务到包这个顺序来提交或回滚。 但是，在内部事务提交后，如果外部事务中止，已提交的事务不会回滚。  
  
### <a name="example-of-multiple-transactions-in-a-package"></a>单个包中的多个事务的示例 
 例如，某个包包含一个序列容器，该序列容器中又存储有两个 Foreach 循环容器，而后面这两个容器中又分别包含两个执行 SQL 任务。 序列容器支持事务，而 Foreach 循环容器则不支持事务，但执行 SQL 任务支持。 在此示例中，每个执行 SQL 任务都将启动自己的事务，如果序列任务上的事务被中止，则执行 SQL 任务将不会回滚。  
  
 序列容器、Foreach 循环容器和执行 SQL 任务的 TransactionOption 属性按照如下方式进行设置：  
  
-   序列容器的 TransactionOption 属性设置为 **Required**。  
  
-   Foreach 循环容器的 TransactionOption 属性设置为 **NotSupported**。  
  
-   执行 SQL 任务的 TransactionOption 属性设置为 **Required**。  
  
 下面的关系图显示了包中的五个不相关的事务。 一个事务是由序列容器启动的，其余四个事务是由执行 SQL 任务启动的。  
  
 ![多个事务的实现](../integration-services/media/mw-dts-trans2.gif "Implementation of multiple transactions")  
 
## <a name="inherited-transactions"></a>继承的事务
 一个包可以使用执行包任务运行另一个包。 子包也就是执行包任务所运行的包，它可以创建自己的包事务，也可以继承父包事务。  
  
 如果同时满足下面这两个条件，则子包会继承父包事务：  
  
-   该包由执行包任务调用。  
  
-   调用该包的执行包任务同时还联接父包事务。  
  
 子包中的容器和任务无法联接父包事务，除非子包本身联接该事务。  
  
### <a name="example-of-inherited-transactions"></a>继承的事务的示例  
 在下面的关系图中，三个包都使用事务。 每个包包含多项任务。 为了强调事务的行为，只显示了执行包任务。 包 A 运行包 B 和包 C。而包 B 运行包 D 和包 E，包 C 运行包 F。  
  
 包和任务具有下列事务属性：  
  
-   对于包 A 和包 C，**TransactionOption** 设置为 **Required** 。  
  
-   对于包 B 和包 D 以及任务执行包 B、执行包 D 和执行包 F，**TransactionOption** 设置为 **Supported** 。  
  
-   对于包 E 以及任务执行包 C 和执行包 E，**TransactionOption** 设置为 **NotSupported** 。  
  
 ![继承的事务流](../integration-services/media/mw-dts-executepack.gif "Flow of inherited transactions")  
  
 只有包 B、包 D 和包 F 可以从它们的父包继承事务。  
  
 包 B 和包 D 继承包 A 启动的事务。  
  
 包 F 继承包 C 启动的事务。  
  
 包 A 和包 C 控制它们自己的事务。  
  
 包 E 不使用事务。  
 
  
## <a name="external-resources"></a>外部资源  
  
-   www.mssqltips.com 上的博客项 [How to Use Transactions in SQL Server Integration Services SSIS](http://go.microsoft.com/fwlink/?LinkId=157783)（如何在 SQL Server Integration Services SSIS 中使用事务）  
  
## <a name="see-also"></a>另请参阅  
 [继承的事务](http://msdn.microsoft.com/library/90db5564-d41e-4cfe-8c9e-4e68d41eff1c)   
 [多个事务](http://msdn.microsoft.com/library/c3664a94-be89-40c0-a3a0-84b74a7fedbe)  
  
  
