---
title: 项目和包的部署 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a2212b44af9eb17625ef296deb9d6223deb313e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62890250"
---
# <a name="deployment-of-projects-and-packages"></a>项目和包的部署
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支持两种部署模型：项目部署模型和包部署模型。 项目部署模型使您可以将项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。  
  
 有关将项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的详细信息，请参阅 [将项目部署到 Integration Services 服务器](../deploy-projects-to-integration-services-server.md)。  
  
 有关包部署模型的详细信息，请参阅[包部署&#40;SSIS&#41;](legacy-package-deployment-ssis.md)。  
  
## <a name="compare-project-deployment-and-package-deployment"></a>比较项目部署和包部署  
 您为项目选择的部署模型的类型将决定可用于该项目的开发和管理选项。 下表显示使用项目部署模型和使用包部署模型之间的差异和相似之处。  
  
|在使用项目部署模型时|使用包部署模型时|  
|---------------------------------------------|---------------------------------------------|  
|项目是部署单元。|包是部署单元。|  
|参数用于向包属性赋值。|配置用于向包属性赋值。|  
|将包含包和参数的项目生成为一个项目部署文件（.ispac 扩展名）。|包（.dtsx 扩展名）和配置（.dtsConfig 扩展名）单独保存到文件系统中。|  
|将包含包和参数的项目部署到 SQL Server 实例上的 SSISDB 目录中。|包和配置复制到另一台计算机上的文件系统中。 包也可以保存到 SQL Server 实例上的 MSDB 数据库中。|  
|数据库引擎需要 CLR 集成。|数据库引擎不需要 CLR 集成。|  
|特定于环境的参数值存储于环境变量中。|特定于环境的配置值存储于配置文件中。|  
|可在执行前在服务器上验证目录中的项目和包。 可以使用 SQL Server Management Studio、存储过程或托管代码执行该验证。|恰好在执行之前对包进行验证。 还可以使用 dtExec 或托管代码验证包。|  
|通过对数据库引擎启动执行，来执行包。 在开始执行前，将项目标识符、显式参数值（可选）和环境引用（可选）分配给某一执行。<br /><br /> 还可以使用 `dtExec` 执行包。|使用 `dtExec` 和 `DTExecUI` 执行实用工具执行包。 适用配置是通过命令提示符参数（可选）来标识的。|  
|在执行过程中，包生成的事件将自动捕获并保存到目录中。 您可以使用 TRANSACT-SQL 视图查询这些事件。|在执行过程中，包生成的事件不自动捕获。 日志提供程序必须添加到包以便捕获事件。|  
|包在单独的 Windows 进程中运行。|包在单独的 Windows 进程中运行。|  
|SQL Server 代理用于计划包执行。|SQL Server 代理用于计划包执行。|  
  
## <a name="features-of-project-deployment-model"></a>项目部署模型的功能  
 下表列出的功能仅可用于为项目部署模型开发的项目。  
  
|功能|Description|  
|-------------|-----------------|  
|Parameters|参数指定包将使用的数据。 您可以分别使用包参数和项目参数将参数范围限定在包级别或项目级别。 参数可用于表达式或任务中。 在将项目部署到目录时，可为每个参数分配文字值，或者使用在设计时分配的默认值。 还可以引用环境变量来代替文字值。 在包执行时解析环境变量值。|  
|环境|环境是可由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目引用的变量的容器。 每个项目可以具有多个环境引用，但包执行的单个实例只能引用来自单个环境的变量。 环境允许您对分配给包的值进行组织。 例如，您可以具有名为“开发”、“测试”和“生产”的环境。|  
|环境变量|环境变量定义可在包执行过程中赋给参数的文字值。 若要使用某一环境变量，请创建环境引用（在与具有参数的环境相对应的项目中），向该环境变量的名称分配某一参数值，并且在配置执行实例时指定相应的环境引用。|  
|SSISDB 目录|所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象都在某一 SQL Server 实例上称作 SSISDB 目录的数据库中进行存储和管理。 通过该目录，您可以使用文件夹组织您的项目和环境。 每个 SQL Server 实例可具有一个目录。 每个目录中可具有零个或多个文件夹。 每个文件夹可具有零个或多个项目以及零个或多个环境。 该目录中的文件夹也可以用作针对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象的权限的边界。|  
|目录存储过程和视图|可以使用大量存储过程和视图来管理该目录中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象。 例如，您可以指定参数和环境变量值，创建和启动执行，以及监视目录操作。 您甚至可以精确看到在执行开始前将由包使用的值。|  
  
## <a name="project-deployment"></a>项目部署  
 项目部署模型的中心是项目部署文件（.ispac 扩展名）。 该项目部署文件是自包含的部署单元，仅包含与项目中的包和参数有关的基本信息。 该项目部署文件不捕获在 Integration Services 项目文件（.dtproj 扩展名）中包含的所有信息。 例如，您用于撰写备注的附加文本文件不存储于该项目部署文件中，因此不部署到目录中。  
  
## <a name="required-tasks"></a>所需磁盘数  
  
-   [将项目部署到 Integration Services 服务器](../deploy-projects-to-integration-services-server.md)  
  
## <a name="related-content"></a>相关内容  
 mattmasson.com 上的博客文章 [考虑一下针对 SSIS 项目的分支策略](https://go.microsoft.com/fwlink/?LinkId=245739)。  
  
## <a name="see-also"></a>请参阅  
 [dtexec 实用工具](dtexec-utility.md)  
  
  
