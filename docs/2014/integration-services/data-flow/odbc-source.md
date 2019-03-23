---
title: ODBC 源 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d125a725a9e1c0cab34c7066fd9554ef0099d6e6
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382070"
---
# <a name="odbc-source"></a>ODBC 源
  ODBC 源通过使用数据库表、视图或 SQL 语句，从支持 ODBC 的数据库中提取数据。  
  
 ODBC 源具有以下数据访问模式用于提取数据：  
  
-   表或视图。  
  
-   SQL 语句的运行结果。  
  
 源使用 ODBC 连接管理器，它指定要使用的访问接口。  
  
 ODBC 源包含源数据输出列。 当 ODBC 目标中的输出列映射到目标列中时，如果没有任何输出列映射到目标列，可能会出现错误。 可以映射不同类型的列，但是，如果输出数据与目标不兼容，则在运行时会出现错误。 根据错误行为，将忽略对错误的设置，并且导致失败，或者行将发送到错误输出。  
  
 ODBC 源有一个常规输出和一个错误输出。  
  
## <a name="error-handling"></a>错误处理  
 ODBC 源有一个错误输出。 组件的错误输出包括以下输出列：  
  
-   **错误代码**:与当前错误相对应的编号。 有关错误的列表，请参阅您正在使用的支持 ODBC 的数据库文档。 有关 SSIS 错误代码的列表，请参阅 SSIS 错误代码和消息参考。  
  
-   **错误列**:导致错误 （针对转换错误） 的源列。  
  
-   标准的输出数据列。  
  
 根据错误行为设置，CDC 源支持在错误输出中返回在提取过程中发生的错误（数据转换、截断）。 有关详细信息，请参阅 [ODBC 目标编辑器（“连接管理器”页）](../odbc-destination-editor-connection-manager-page.md)。  
  
## <a name="data-type-support"></a>数据类型支持  
 有关 ODBC 源支持的数据类型的信息，请参阅 Connector for Open Database Connectivity (ODBC) by Attunity。  
  
## <a name="extract-options"></a>提取选项  
 ODBC 源在“批处理”或“逐行”模式下操作。 使用的模式由 **FetchMethod** 属性确定。 下表对这些模式进行了说明。  
  
-   **批处理**:组件将尝试使用最高效的提取方法基于发现的 ODBC 访问接口功能。 对于大多数现今的 ODBC 提供程序，这是具有数组绑定的 SQLFetchScroll（其中，数组大小由 **BatchSize** 属性确定）。 如果选择“批处理”并且提供程序不支持此方法，则 ODBC 目标将自动切换到“逐行”模式。  
  
-   **行由行**:组件使用 SQLFetch 来一次检索行。  
  
 有关 **FetchMethod** 属性的详细信息，请参阅 [ODBC Source Custom Properties](odbc-source-custom-properties.md)。  
  
## <a name="parallelism"></a>Parallelism  
 对于可对同一台计算机或不同计算机（并非一般的全局会话限制）上的相同表或不同表并行运行的 ODBC 源组件的数目没有限制。  
  
 但是，要使用的 ODBC 访问接口的限制可能会限制通过该访问接口的同时连接的数目。 这些限制将会限制 ODBC 源可能支持的并行实例的数目。 SSIS 开发人员必须知道要使用的任何 ODBC 访问接口的限制并且在生成 SSIS 包时将这些限制元素考虑进去。  
  
## <a name="troubleshooting-the-odbc-source"></a>ODBC 源故障排除  
 可以记录 ODBC 源对外部数据访问接口所做的调用。 利用此日志记录功能，可以对 ODBC 源执行的从外部数据源加载数据的操作进行故障排除。 若要记录 ODBC 源对外部数据访问接口进行的调用，请启用 ODBC 驱动程序管理器跟踪。 有关详细信息，请参阅 Microsoft 文档 *数据源管理员如何使用 ODBC 生成 ODBC 跟踪*。  
  
## <a name="configuring-the-odbc-source"></a>配置 ODBC 源  
 您可以通过编程方式或者通过 SSIS 设计器配置 ODBC 源。  
  
 有关详细信息，请参阅下列主题之一：  
  
-   [ODBC 源编辑器（“连接管理器”页）](../odbc-source-editor-connection-manager-page.md)  
  
-   [ODBC 源编辑器（“列”页）](../odbc-source-editor-columns-page.md)  
  
-   [ODBC 源编辑器（“错误输出”页）](../odbc-source-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框包含可通过编程方式设置的属性。  
  
 打开 **“高级编辑器”** 对话框：  
  
-   在您的 **项目的** “数据流” [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 屏幕上，右键单击 ODBC 源，然后选择 **“显示高级编辑器”**。  
  
 有关可在“高级编辑器”对话框中设置的属性的详细信息，请参阅 [ODBC Source Custom Properties](odbc-source-custom-properties.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [ODBC 源编辑器（“错误输出”页）](../odbc-source-editor-error-output-page.md)  
  
-   [ODBC 源编辑器（“列”页）](../odbc-source-editor-columns-page.md)  
  
-   [ODBC 源编辑器（“连接管理器”页）](../odbc-source-editor-connection-manager-page.md)  
  
-   [使用 ODBC 源提取数据](odbc-source.md)  
  
-   [ODBC Source Custom Properties](odbc-source-custom-properties.md)  
  
  
