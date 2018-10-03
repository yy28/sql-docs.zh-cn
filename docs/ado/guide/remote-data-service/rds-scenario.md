---
title: RDS 方案 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aaeedb6dffb992ac940eebd450c63d33badb299d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845275"
---
# <a name="rds-scenario"></a>RDS 方案
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 通讯簿应用程序是一种方案演示如何使用远程数据服务 (RDS) 来构建简单、 感知数据的 Web 应用程序 — 联机公司通讯簿。 此方案可用于 Microsoft Visual Basic Scripting Edition (VBScript) 和 COM 的编程人员，以便了解如何使用 RDS，感知数据的 ActiveX 控件，更有经验的软件开发者要生成以数据为中心的 Web 应用程序。  
  
 此方案假定你知道如何使用 ActiveX 控件的基本 HTML 布局标记、 使用 DHTML 数据绑定技术和程序。  
  
 如果已安装 SDK，可以在 samples\dataaccess\rds\AddressBook\AddressBook.asp SDK 目录中找到通讯簿示例应用程序的完整源代码。 若要查看通讯簿方案，请在 Internet Explorer 4.0 或更高版本中，键入**http://*webserver*/RDS/AddressBook/AddressBook.asp**其中*web 服务器*是提供的名称到 Windows NT 4.0 或 Windows 2000 Web 服务器计算机运行 Internet Information Services (IIS) 和 ASP。  
  
## <a name="introduction-to-address-book"></a>通讯簿简介  
 通讯簿示例应用程序提供了可用于通过 intranet 进行发布的可搜索目录是简单的联机通讯簿。 通讯簿旨在使用户可以请求员工有关的信息的一个或多个字段中输入搜索字符串。 若要显示的基本功能的远程数据服务，示例应用程序有意保持小，具有最小数量的对象和搜索字段。  
  
 应用程序界面由以下几个部分组成：  
  
-   非可视**rds。DataControl**客户端用于连接到数据库的数据绑定对象。  
  
-   充当员工属性搜索条件的输入字段的 HTML 文本框。  
  
-   HTML 命令按钮可以生成查询，清除搜索字段，包含员工信息更新数据库、 取消挂起的更改，并导航的网格中显示的数据行。  
  
-   DHTML 数据绑定来显示数据从查询返回的对后端数据库 (通过**rds。DataControl**数据绑定对象) 的表中。  
  
-   VBScript 例程，连接每个元素前面所述，并允许它们进行交互。 VBScript 代码还用于初始化**rds。DataControl**对象，并动态创建 HTML 表的名称中的列标题**rds。DataControl**记录集字段。  
  
 单击链接，从步骤到步骤来设置和运行的应用场景，以及若要了解有关方案的工作方式的详细信息。  
  
 此方案包含以下主题。  
  
-   [通讯簿应用程序的系统要求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [运行通讯簿 SQL 脚本](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [运行通讯簿示例应用程序](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [通讯簿数据绑定对象](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [通讯簿命令按钮](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [通讯簿导航按钮](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>请参阅  
 [通讯簿应用程序的系统要求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX 数据对象 (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)


