---
title: 结果集映射到变量中执行 SQL 任务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- mapping result sets to variables [Integration Services]
- variables [Integration Services], mapping result sets to
ms.assetid: f76738b6-dc75-4ff9-a3dd-8b083d8e410e
caps.latest.revision: 28
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cdd76b3f0b1665fa6336e82536ca474c0b5e1fab
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277373"
---
# <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>在执行 SQL 任务中将结果集映射到变量
  本主题介绍如何在执行 SQL 任务中创建结果集和变量之间的映射。 将结果集映射到变量以便使结果集对包中其他元素可用。 例如，脚本任务中的脚本可以读取该变量，然后使用结果集中的值，或者 XML 源可以使用集存储在变量中的结果。 如果结果集是由父包生成的，那么通过将结果集映射到父包中的变量，然后在子包中创建父包变量配置以存储父变量值，就可以使结果集对执行包任务所调用的子包可用。  
  
 有关不同类型的结果集和可以映射到结果集的变量数据类型的说明，请参阅 [执行 SQL 任务中的结果集](control-flow/execute-sql-task.md)。  
  
### <a name="to-map-a-result-set-to-a-variable"></a>将结果集映射到变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在“解决方案资源管理器”中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  如果该包尚未包括执行 SQL 任务，则向该包的控制流中添加一个此类任务。 有关详细信息，请参阅[添加或删除任务或容器中控制流](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  实例时都提供 SQL Server 登录名。  
  
5.  双击执行 SQL 任务。  
  
6.  在 **“执行 SQL 任务编辑器”** 对话框中的 **“常规”** 页上，选择 **“单行”**、 **“完整结果集”** 或 **XML** 结果集类型。  
  
     有关不同的结果集的说明，请参阅 [执行 SQL 任务中的结果集](result-sets-in-the-execute-sql-task.md)  
  
7.  单击 **“结果集”**。  
  
8.  若要添加结果集映射，请单击 **“添加”**。  
  
9. 从 **“变量名称”** 列表中，选择变量或创建新变量。 有关详细信息，请参阅 [添加、删除、更改包中用户定义变量的作用域](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)。  
  
     有关可映射到不同结果集中的变量数据类型的说明，请参阅 [执行 SQL 任务中的结果集](result-sets-in-the-execute-sql-task.md)。  
  
     有关如何将某个变量映射到单个列以及将多个变量映射到多个列的信息，请参阅 **Result Sets in the Execute SQL Task** 中的 [使用结果集填充变量](control-flow/execute-sql-task.md)部分。  
  
10. 在 **“结果名称”** 列表中，可根据需要修改结果集的名称。  
  
     通常，可以将列名用作结果集名称，也可以将列列表中的列的序号位置用作结果集名称。 使用列名作为结果集名称的功能将依赖于配置任务要使用的访问接口。 并非所有访问接口都使列名可用。  
  
11. 单击“确定” 。  
  
## <a name="see-also"></a>请参阅  
 [执行 SQL 任务](control-flow/execute-sql-task.md)   
 [中的结果集执行 SQL 任务](result-sets-in-the-execute-sql-task.md)   
 [执行包任务](control-flow/execute-package-task.md)   
 [包配置](../../2014/integration-services/package-configurations.md)   
 [创建包配置](../../2014/integration-services/create-package-configurations.md)   
 [在子包中使用变量和参数的值](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)   
 [Integration Services &#40;SSIS&#41;变量](integration-services-ssis-variables.md)  
  
  
