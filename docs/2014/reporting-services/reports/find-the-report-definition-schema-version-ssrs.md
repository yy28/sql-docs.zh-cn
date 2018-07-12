---
title: 查找报表定义架构版本 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 42fd97141fad21c9995857a6e51c495cf6eac078
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151908"
---
# <a name="find-the-report-definition-schema-version-ssrs"></a>查找报表定义架构版本 (SSRS)
  报表定义文件为用于验证 rdl 文件的报表定义架构的版本指定 RDL 命名空间。 当在报表创作环境（如 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的报表设计器或报表生成器）中打开某个 .rdl 文件时，如果报表是针对先前命名空间创建的，会自动创建一个备份文件，并将该报表升级到当前命名空间。 如果保存升级后的报告定义，则同时还会保存转换后的 .rdl 文件。 这是升级报表定义的唯一方法。 报表定义本身在报表服务器上不升级。 已编译的报表在报表服务器上升级。 有关更多信息，请参见 [Upgrade Reports](../install-windows/upgrade-reports.md)。  
  
### <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>如何确定报表的 RDL 架构版本  
  
1.  在某个能够查看 xml 的应用程序（如记事本或 XML Notepad 2007）中打开报表 .rdl 文件。  
  
     XML REPORT 元素指定架构命名空间。 例如，下面的 Report 元素指定报表设计器的命名空间以及报表定义的命名空间。  
  
    ```  
    <Report xmlns:rd=http://schemas.microsoft.com/SQLServer/reporting/reportdesigner   
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     以下 URL 指定了报表定义命名空间： `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`。  
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>如何确定报表设计器的 RDL 架构版本  
  
1.  打开一个新项目。 您选择的项目版本决定 RDL 架构的版本。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，支持多个架构版本。 有关详细信息，请参阅 [SQL Server Data Tools 中的部署和版本支持 (SSRS)](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)中。  
  
2.  在 **“项目”** 菜单上，单击 **“添加新项”**。 **“添加新项”** 对话框将会打开。  
  
3.  在 **“模板”** 窗格中，单击 **“报表”**。  
  
4.  在 **“名称”** 中，键入报表名称，或接受默认名称。  
  
5.  单击 **“添加”**。 报表设计器将在“设计”视图中打开一个新的空白报表。  
  
6.  在 **“视图”** 菜单上，单击 **“代码”**。 该报告定义将显示为一个 XML 文件。  
  
     XML REPORT 元素指定架构命名空间。 例如，下面的 Report 元素指定报表设计器的命名空间以及报表定义的命名空间。  
  
    ```  
    <Report xmlns:rd=http://schemas.microsoft.com/SQLServer/reporting/reportdesigner  
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     以下 URL 指定了报表定义命名空间： `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
### <a name="how-to-identify-the-rdl-schema-version-on-the-report-server"></a>如何确定报表服务器上的 RDL 架构版本  
  
-   在报表管理器中，键入报表服务器的 URL。 例如，以下 URL 指定一个本地计算机上的报表服务器：  
  
     `http://localhost/reportserver/reportdefinition.xsd`  
  
     将在浏览器中打开 .xsd 文件。  
  
     XML schema 元素指定架构命名空间。 例如，下面的架构元素指定三个命名空间：由 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]内部使用的 targetNamespace 引用、架构自身 (xsd) 的 xsd 引用以及报表定义引用。  
  
    ```  
    <xsd:schema   
    targetNamespace="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    elementFormDefault="qualified">  
    ```  
  
     以下 URL 指定了报表定义命名空间： `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
## <a name="see-also"></a>请参阅  
 [升级报表](../install-windows/upgrade-reports.md)   
 [报表定义语言 (SSRS)](report-definition-language-ssrs.md)  
  
  
