---
title: RDS 方案 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: rothja
ms.author: jroth
ms.openlocfilehash: d73bb03ceb08e61257c0e4fc6d3f6a627ddb746d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763578"
---
# <a name="rds-scenario"></a>RDS 方案
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 通讯簿应用程序是一种方案，演示如何使用远程数据服务（RDS）构建一个简单的数据感知 Web 应用程序，即联机企业通讯簿。 此方案对于想要了解如何将数据感知 ActiveX 控件与 RDS 一起使用的 Microsoft Visual Basic Scripting Edition （VBScript）和 COM 程序员非常有用，还适用于需要构建以数据为中心的 Web 应用程序的更有经验的软件开发人员。  
  
 此方案假设你知道如何使用基本 HTML 布局标记，如何使用 DHTML 数据绑定技术，以及如何使用 ActiveX 控件编程。  
  
 如果已安装 SDK，则可以在 SDK 目录的 samples\dataaccess\rds\AddressBook\AddressBook.asp. 中找到通讯簿示例应用程序的完整源代码。 若要查看通讯簿方案，请在 Internet Explorer 4.0 或更高版本中，键入**https://*web*服务器/RDS/AddressBook/AddressBook.asp** ，其中， *web*服务器是向运行 Internet Information Services （IIS）和 Asp 的 Windows NT 4.0 或 windows 2000 Web 服务器计算机提供的名称。  
  
## <a name="introduction-to-address-book"></a>通讯簿简介  
 通讯簿示例应用程序提供了一个简单的联机通讯簿，可用于通过 intranet 发布可搜索的目录。 通讯簿的设计使用户可以在一个或多个字段中输入搜索字符串来请求有关员工的信息。 为了向您展示远程数据服务的基本功能，示例应用程序有意保存为小，并具有最小数量的对象和搜索字段。  
  
 应用程序接口由以下部分组成：  
  
-   非 visual **RDS。DataControl**用于连接到数据库的客户端使用的数据绑定对象。  
  
-   作为员工属性搜索条件的输入字段的 HTML 文本框。  
  
-   用于生成查询、清除搜索字段、用员工信息更新数据库、取消挂起的更改，以及导航网格中显示的数据行的 HTML 命令按钮。  
  
-   用于显示针对后端数据库的查询返回的数据的 DHTML 数据绑定（通过**RDS。DataControl**数据绑定对象）。  
  
-   VBScript 例程连接前面提到的每个元素，并允许它们进行交互。 VBScript 代码还用于初始化**RDS。DataControl**对象，并从 RDS 的名称以动态方式创建 HTML 表中的列标题 **。DataControl**记录集字段。  
  
 请按照步骤中的链接来设置和运行方案，并详细了解该方案的工作原理。  
  
 此方案包含以下主题。  
  
-   [通讯簿应用程序的系统要求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [运行通讯簿 SQL 脚本](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [运行通讯簿示例应用程序](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [通讯簿数据绑定对象](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [通讯簿命令按钮](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [通讯簿导航按钮](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>另请参阅  
 [通讯簿应用程序的系统要求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX 数据对象（ADO）](../../../ado/microsoft-activex-data-objects-ado.md)   
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)


