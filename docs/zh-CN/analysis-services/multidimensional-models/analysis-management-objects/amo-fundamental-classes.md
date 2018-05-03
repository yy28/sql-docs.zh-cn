---
title: AMO 基础类 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ffa7973757ce41a3975bcbb70170679109527e42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="amo-fundamental-classes"></a>AMO Fundamental 类
  基础类是使用分析管理对象 (AMO) 的起点。 通过这些类，您可以为将在应用程序中使用的其他对象建立自己的环境。 基础类包括以下对象：<xref:Microsoft.AnalysisServices.Server>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.DataSource> 和 <xref:Microsoft.AnalysisServices.DataSourceView>。  
  
 下图显示了本主题中介绍的类之间的关系。  
  
 ![AMO 基础类](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-fundamentalclasses.gif "AMO 基础类")  
  
 本主题包含以下各节：  
  
-   [服务器对象](#ServerObjects)  
  
-   [数据库对象](#DatabaseObjects)  
  
-   [数据源和 DataSourceView 对象](#DSandDSV)  
  
##  <a name="ServerObjects"></a> 服务器对象  
 另外，还具有对以下方法的访问权限：  
  
-   连接管理：Connect、Disconnect、Reconnect 和 GetConnectionState。  
  
-   事务管理：BeginTransaction、CommitTransaction 和 RollbackTransaction。  
  
-   Backup 和 Restore。  
  
-   DDL 执行：Execute、CancelCommand、SendXmlaRequest、StartXmlaRequest。  
  
-   元数据管理：UpdateObjects 和 Validate。  
  
 若要连接到服务器，与在 ADOMD.NET 和 OLEDB 中使用一样，需要一个标准的连接字符串。 有关详细信息，请参阅<xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>。 服务器的名称可指定为连接字符串，无需使用连接字符串格式。  
  
 有关可用的方法和属性的详细信息，请参阅 <xref:Microsoft.AnalysisServices.Server> 中的 <xref:Microsoft.AnalysisServices>。  
  
##  <a name="DatabaseObjects"></a> 数据库对象  
 若要在应用程序中使用 <xref:Microsoft.AnalysisServices.Database> 对象，必须从父服务器数据库集合获得一个数据库实例。 若要创建数据库，可向服务器数据库集合添加一个 <xref:Microsoft.AnalysisServices.Database> 对象，并将新实例更新到服务器。 若要删除数据库，可使用 <xref:Microsoft.AnalysisServices.Database> 对象自己的 Drop 方法将其删除。  
  
 可使用 BackUp 方法备份数据库（从 <xref:Microsoft.AnalysisServices.Database> 对象或 <xref:Microsoft.AnalysisServices.Server> 对象），但使用 Restore 方法仅可从 <xref:Microsoft.AnalysisServices.Server> 对象还原数据库。  
  
 有关可用的方法和属性的详细信息，请参阅 <xref:Microsoft.AnalysisServices.Database> 中的 <xref:Microsoft.AnalysisServices>。  
  
##  <a name="DSandDSV"></a> 数据源和 DataSourceView 对象  
 数据源是使用数据库类的 <xref:Microsoft.AnalysisServices.DataSourceCollection> 管理的。 可从 <xref:Microsoft.AnalysisServices.DataSource> 对象使用 Add 方法创建 <xref:Microsoft.AnalysisServices.DataSourceCollection> 实例。 可从 <xref:Microsoft.AnalysisServices.DataSource> 对象使用 Remove 方法删除 <xref:Microsoft.AnalysisServices.DataSourceCollection> 实例。  
  
 <xref:Microsoft.AnalysisServices.DataSourceView> 对象是从数据库类的 <xref:Microsoft.AnalysisServices.DataSourceViewCollection> 对象管理的。  
  
 有关可用的方法和属性的详细信息，请参阅 <xref:Microsoft.AnalysisServices.DataSource> 中的 <xref:Microsoft.AnalysisServices.DataSourceView> 和 <xref:Microsoft.AnalysisServices>。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices>   
 [引入 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [编程 AMO Fundamental Objects](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-fundamental-objects.md)  
  
  
