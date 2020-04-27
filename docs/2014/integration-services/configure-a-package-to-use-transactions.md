---
title: 将包配置为使用事务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], configuring packages to use
ms.assetid: 8bf14957-27b4-456b-81d9-e1a0e0ca94b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 16d1f0f4c24f18327ee31da1fb85a74d19588384
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060862"
---
# <a name="configure-a-package-to-use-transactions"></a>将包配置为使用事务
  将包配置为使用事务时，您有两种选择：  
  
-   包仅包含单个事务。 在这种情况下，将由包自身“启动” ** 此事务，而此包中的各个任务和容器参与此单个事务。  
  
-   包包含多个事务。 在这种情况下，包支持多个事务，但这些事务实际上是由包中的各个任务或容器启动的。  
  
 下面的过程介绍如何配置上述两种选择。  
  
## <a name="configuring-a-single-transaction"></a>配置单个事务  
 在此选择中，程序包自身启动单个事务。 通过将包的 TransactionOption 属性设置为`Required`，可以将包配置为启动此事务。  
  
 接着，在此单个事务中登记特定任务和容器。 若要在事务中登记任务或容器，请将该任务或容器的 TransactionOption 属性设置为`Supported`。  
  
#### <a name="to-configure-a-package-to-use-a-single-transaction"></a>将包配置为使用单个事务  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要配置为使用事务的包所在的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  右键单击控制流设计图面背景中的任意位置，然后单击“属性”****。  
  
5.  在 "**属性**" 窗口中，将 "TransactionOption `Required`" 属性设置为。  
  
6.  在“控制流”**** 选项卡的设计图面上，右键单击要在事务中注册的任务或容器，再单击“属性”****。  
  
7.  在 "**属性**" 窗口中，将 "TransactionOption `Supported`" 属性设置为。  
  
    > [!NOTE]  
    >  若要在事务中登记连接，请注册在该事务中使用连接的任务。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](connection-manager/integration-services-ssis-connections.md)。  
  
8.  对要在事务中注册的每个任务和容器，请重复步骤 6 和 7。  
  
## <a name="configuring-multiple-transactions"></a>配置多个事务  
 在此选择中，包自身支持但不启动事务。 通过将包的 TransactionOption 属性设置为`Supported`，可以将包配置为支持事务。  
  
 接着，在包中将所需任务和容器配置为启动或参与事务。 若要将任务或容器配置为启动事务，请将该任务或容器的 TransactionOption 属性设置为`Required`。  
  
#### <a name="to-configure-a-package-to-use-multiple-transactions"></a>将包配置为使用多个事务  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要配置为使用事务的包所在的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  右键单击控制流设计图面背景中的任意位置，然后单击“属性”****。  
  
5.  在 "**属性**" 窗口中，将 "TransactionOption `Supported`" 属性设置为。  
  
    > [!NOTE]  
    >  该包支持事务，但事务是由包中的任务或容器启动的。  
  
6.  在“控制流”**** 选项卡的设计图面上，右键单击要为其启动事务的包中的任务或容器，然后单击“属性”****。  
  
7.  在 "**属性**" 窗口中，将 "TransactionOption `Required`" 属性设置为。  
  
8.  如果事务由容器启动，则右键单击要在事务中注册的任务或容器，然后单击“属性”****。  
  
9. 在 "**属性**" 窗口中，将 "TransactionOption `Supported`" 属性设置为。  
  
    > [!NOTE]  
    >  若要在事务中登记连接，请注册在该事务中使用连接的任务。 有关详细信息，请参阅 [Integration Services (SSIS) 连接](connection-manager/integration-services-ssis-connections.md)。  
  
10. 对启动事务的每个任务和容器，请重复步骤 6 到 9。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 事务](integration-services-transactions.md)  
  
  
