---
title: DataReader 目标 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.datareaderdest.f1
helpviewer_keywords:
- DataReader destination
- destinations [Integration Services], DataReader
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe2c9335eeb25fec264e2750dc1f9487ca53ff80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726987"
---
# <a name="datareader-destination"></a>DataReader 目标

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  DataReader 目标使用 ADO.NET **DataReader** 接口显示数据流中的数据。 此数据然后可由其他应用程序占用。 例如，可以将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表的数据源配置为使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的运行结果。 若要执行此操作，请创建实现 DataReader 目标的数据流。  
  
 有关以编程方式访问和读取 DataReader 目标中的值的信息，请参阅 [加载本地包的输出](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)。  
  
## <a name="configuration-of-the-datareader-destination"></a>DataReader 目标的配置  
 可以指定 DataReader 目标的超时值，并指示如果发生超时目标是否失败。 如果应用程序在指定时间内不请求数据，则出现超时。  
  
 DataReader 目标具有一个输入。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [DataReader 目标自定义属性](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
  
