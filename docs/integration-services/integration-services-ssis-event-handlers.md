---
title: "Integration Services (SSIS) 事件处理程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 包, 事件"
  - "运行时 [Integration Services]"
  - "SQL Server Integration Services 包, 事件"
  - "事件处理程序 [Integration Services], 关于事件处理程序"
  - "事件 [Integration Services]"
  - "包 [Integration Services], 事件"
  - "事件处理程序 [Integration Services]"
  - "SSIS 包, 事件"
  - "容器 [Integration Services], 事件"
  - "事件 [Integration Services], 关于事件"
ms.assetid: 6f60cf93-35dc-431c-908d-2049c4ab66ba
caps.latest.revision: 52
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 51
---
# Integration Services (SSIS) 事件处理程序
  在运行时，可执行文件（包以及 Foreach 循环容器、For 循环容器、序列容器和任务宿主容器）会引发事件。 例如，错误发生时会引发 OnError 事件。 可以为这些事件创建自定义事件处理程序，以扩展包的功能并使包在运行时更容易管理。 事件处理程序可以执行诸如下列任务：  
  
-   当包或任务运行完成时清除临时数据存储。  
  
-   在包运行前检索系统信息，以便评估资源可用性。  
  
-   在引用表中的查找失败时刷新表中的数据。  
  
-   当发生错误或警告时，或者当任务失败时，发送电子邮件。  
  
 如果事件没有事件处理程序，则将该事件提升到包中容器层次结构中的上一级容器。 如果此容器具有事件处理程序，则该事件处理程序当事件发生时运行。 如果没有，则将该事件提升到容器层次结构中的上一级容器。  
  
 以下关系图显示具有 For 循环容器的简单包，该容器包含一个执行 SQL 任务。  
  
 ![包、For 循环、任务宿主和执行 SQL 任务](../integration-services/media/mw-dts-eventhandlerpkg.gif "包、For 循环、任务宿主和执行 SQL 任务")  
  
 只有包具有事件处理程序，用于处理其 **OnError** 事件。 如果执行 SQL 任务运行时发生错误，包的 **OnError** 事件处理程序就会运行。 以下关系图显示导致包的 **OnError** 事件处理程序执行的调用序列。  
  
 ![事件处理程序流](../integration-services/media/mw-dts-eventhandlers.gif "事件处理程序流")  
  
 事件处理程序是事件处理程序集的成员，所有容器都包含此事件处理程序集。 如果使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器创建包，就可以在 **设计器的** “包资源管理器” **选项卡上的** “事件处理程序” [!INCLUDE[ssIS](../includes/ssis-md.md)] 文件夹中看到事件处理程序集的成员。  
  
 可以采用下列方法配置事件处理程序容器：  
  
-   指定事件处理程序的名称和说明。  
  
-   指示事件处理程序是否运行，事件处理程序失败时包是否失败，以及事件处理程序失败前可发生的错误数。  
  
-   指定返回执行结果，而不是事件处理程序在运行时返回的实际执行结果。  
  
-   指定事件处理程序的事务选项。  
  
-   指定事件处理程序使用的日志记录模式。  
  
## 事件处理程序内容  
 创建事件处理程序与生成包类似；事件处理程序具有多个任务和容器，这些任务和容器按照一定顺序组织成控制流，事件处理程序也可以包含多个数据流。 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器包含 **“事件处理程序”** 选项卡，用于创建自定义事件处理程序。  
  
 还可以采用编程方式创建事件处理程序。 有关详细信息，请参阅[以编程方式处理事件](../integration-services/building-packages-programmatically/handling-events-programmatically.md)。  
  
## 运行时事件  
 下表列出 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供的事件处理程序，并介绍导致事件处理程序运行的运行时事件。  
  
|事件处理程序|事件|  
|-------------------|-----------|  
|**OnError**|**OnError** 事件的事件处理程序。 此事件在发生错误时由可执行文件引发。|  
|**OnExecStatusChanged**|**OnExecStatusChanged** 事件的事件处理程序。 此事件在其执行状态更改时由可执行文件引发。|  
|**OnInformation**|**OnInformation** 事件的事件处理程序。 此事件在可执行文件的验证和执行期间引发以报告信息。 此事件仅传递信息，不传递错误或警告。|  
|**OnPostExecute**|**OnPostExecute** 事件的事件处理程序。 此事件由可执行文件在其运行完成后立即引发。|  
|**OnPostValidate**|**OnPostValidate** 事件的事件处理程序。 此事件由可执行文件在其验证完成时引发。|  
|**OnPreExecute**|**OnPreExecute** 事件的事件处理程序。 此事件由可执行文件在其运行前引发。|  
|**OnPreValidate**|**OnPreValidate** 事件的事件处理程序。 此事件由可执行文件在其验证开始时引发。|  
|**OnProgress**|**OnProgress** 事件的事件处理程序。 此事件由可执行文件在其完成可度量的进度时引发。|  
|**OnQueryCancel**|**OnQueryCancel** 事件的事件处理程序。 此事件由可执行文件引发，以确定它是否应停止运行。|  
|**OnTaskFailed**|**OnTaskFailed** 事件的事件处理程序。 此事件由任务在其失败时引发。|  
|**OnVariableValueChanged**|**OnVariableValueChanged** 事件的事件处理程序。 此事件在变量值更改时由可执行文件引发。 此事件由此变量的可执行文件引发。 如果将变量的 **RaiseChangeEvent** 属性设置为 **False**，则不引发此事件。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../integration-services/integration-services-ssis-variables.md)。|  
|**OnWarning**|**OnWarning** 事件的事件处理程序。 此事件在发生警告时由可执行文件引发。|  
  
## 事件处理程序的配置  
 可以在 **的** “属性” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 窗口中设置属性，或以编程方式设置属性。  
  
 有关如何在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中设置这些属性的信息，请参阅[设置任务或容器的属性](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)。  
  
 有关如何以编程方式设置这些属性的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>。  
  
## 相关任务  
 有关如何向包中添加事件处理程序的信息，请参阅[在包中添加事件处理程序](../Topic/Add%20an%20Event%20Handler%20to%20a%20Package.md)。  
  
  