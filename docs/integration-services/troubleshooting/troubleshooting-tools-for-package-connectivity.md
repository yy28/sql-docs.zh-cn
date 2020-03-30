---
title: 包连接故障排除工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- connectivity [Integration Services], troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 08a019f5-8ba7-4527-97c1-e9846d4022ff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 70e53f37056357fbaff315d6cd432b2171eb478b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295062"
---
# <a name="troubleshooting-tools-for-package-connectivity"></a>包连接故障排除工具

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括一些功能和工具，您可以利用它们对在包和包从其提取和加载数据的数据源之间的连接进行故障排除。  
  
## <a name="troubleshooting-issues-with-external-data-providers"></a>外部数据访问接口问题的故障排除  
 很多包在与外部数据访问接口交互时会失败。 但是，这些访问接口返回到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的消息经常无法提供足够的信息来对交互开始进行故障排除。 为了满足此故障排除的需要， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含日志记录消息，这些消息可用来对包与外部数据源的交互进行故障排除。  
  
-   **启用日志记录并选择包的“诊断”事件可以看到故障排除消息**。 下列 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件能够在每次对外部数据访问接口的调用前后向日志写入消息：  
  
    -   OLE DB 连接管理器、OLE DB 源以及 OLE DB 目标  
  
    -   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器和 ADO NET 源  
  
    -   执行 SQL 任务  
  
    -   查找转换、OLE DB 命令转换和渐变维度转换  
  
     日志记录消息包括正被调用的方法的名称。 例如，这些日志消息可能包括 OLE DB **Open** 对象的 **Connection** 方法或 **ExecuteNonQuery** 对象的 **Command** 方法。 该消息具有以下格式，其中 '%1!s!' 是方法信息的占位符：  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: '%1!s!'.  
    ExternalRequest_post: '%1!s!'. The external request has completed.  
    ```  
  
     若要对与外部数据提供程序的交互进行故障排除，请检查日志，以查看每个“之前”消息 (`ExternalRequest_pre`) 是否都具有相对应的“之后”消息 (`ExternalRequest_post`)。 如果没有对应的“之后”消息，就会知道外部数据访问接口不会按预期方式回应。  
  
     下面的示例显示了包含这些日志记录消息的日志中的一些示例行：  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: 'ITransactionJoin::JoinTransaction'.  
    ExternalRequest_post: 'ITransactionJoin::JoinTransaction succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Open'.  
    ExternalRequest_post: 'IDbConnection.Open succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.CreateCommand'.  
    ExternalRequest_post: 'IDbConnection.CreateCommand finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbCommand.ExecuteReader'.  
    ExternalRequest_post: 'IDbCommand.ExecuteReader finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.GetSchemaTable'.  
    ExternalRequest_post: 'IDataReader.GetSchemaTable finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.Close'.  
    ExternalRequest_post: 'IDataReader.Close finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Close'.  
    ExternalRequest_post: 'IDbConnection.Close finished'. The external request has completed."  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [包开发的故障排除工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [包执行的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
