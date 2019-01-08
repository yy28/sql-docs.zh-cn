---
title: ADO NET 目标 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetdest.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aefe3276e11cb4da2523d0e089afc7220eb07ded
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351373"
---
# <a name="ado-net-destination"></a>ADO NET 目标
  ADO NET 目标可将数据加载到各种使用数据库表或视图的兼容 [!INCLUDE[vstecado](../../includes/vstecado-md.md)]的数据库中。 你可以选择将这些数据加载到现有表或视图中，或者先创建一个新表，然后将这些数据加载到新表中。  
  
 可使用 ADO NET 目标连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 不支持使用 OLE DB 连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。 有关 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的详细信息，请参阅 [通用指导原则和限制（Microsoft Azure SQL 数据库）](https://go.microsoft.com/fwlink/?LinkId=248228)。  
  
## <a name="troubleshooting-the-ado-net-destination"></a>ADO NET 目标故障排除  
 可以记录 ADO NET 目标对外部数据访问接口所做的调用。 利用此日志记录功能，可以排除 ADO NET 目标执行将数据保存到外部数据源的操作过程中发生的故障。 若要记录 ADO NET 目标对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ado-net-destination"></a>配置 ADO NET 目标  
 此目标使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器连接到数据源，并且此连接管理器可指定要使用的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 访问接口。 有关详细信息，请参阅 [ADO.NET Connection Manager](../connection-manager/ado-net-connection-manager.md)。  
  
 ADO NET 目标包括输入列和目标数据源中的列之间的映射。 不必将输入列映射到所有目标列。 但是，某些目标列的属性可能需要输入列的映射。 否则，可能会发生错误。 例如，如果目标列不允许出现空值，则必须将输入列映射到该目标列。 另外，映射的列的数据类型必须是兼容的。 例如，如果 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 访问接口不支持将数据类型为字符串的输入列映射到数据类型为数值的目标列，则不能进行此映射。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持将文本插入到数据类型设置为图像的列中。 有关值数据类型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的详细信息，请参阅 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)。  
  
> [!NOTE]  
>  ADO NET 目标不支持将数据类型设置为 DT_DBTIME 的输入列映射到数据类型设置为 datetime 的数据库列。 有关 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的详细信息，请参阅 [Integration Services 数据类型](integration-services-data-types.md)。  
  
 ADO NET 目标具有一个常规输入和一个错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可在 **“ADO NET 目标编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [ADO NET 目标编辑器（“连接管理器”页）](../ado-net-destination-editor-connection-manager-page.md)  
  
-   [ADO NET 目标编辑器（“映射”页）](../ado-net-destination-editor-mappings-page.md)  
  
-   [ADO NET 目标编辑器（“错误输出”页）](../ado-net-destination-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../common-properties.md)  
  
-   [ADO NET 自定义属性](ado-net-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)。  
  
  
