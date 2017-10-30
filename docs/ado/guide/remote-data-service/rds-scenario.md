---
title: "RDS 方案 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 920df727d2714629a45280133c53011afccc5c4d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="rds-scenario"></a>RDS 方案
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 通讯簿应用程序是一种方案演示如何使用远程数据服务 (RDS) 来生成一个简单、 数据识别的 Web 应用程序-联机企业通讯簿。 这种情况下用于 Microsoft Visual Basic Scripting Edition (VBScript) 和 COM 的编程人员想要了解如何使用 RDS，数据识别 ActiveX 控件，并更有经验的软件开发人员要构建以数据为中心的 Web 应用程序。  
  
 此方案假定你知道如何使用 ActiveX 控件的基本的 HTML 布局标记、 使用 DHTML 数据绑定技术和程序。  
  
 如果已安装 SDK，可以在 samples\dataaccess\rds\AddressBook\AddressBook.asp 的 SDK 目录中找到通讯簿示例应用程序的完整源代码。 若要查看的通讯簿方案，Internet Explorer 4.0 版或更高版本中，键入* *http://*web 服务器*/RDS/AddressBook/AddressBook.asp** 其中*web 服务器*是的名称提供给正在运行 Internet Information Services (IIS) 和 ASP 你 Windows NT 4.0 或 Windows 2000 Web 服务器计算机。  
  
## <a name="introduction-to-address-book"></a>通讯簿简介  
 通讯簿示例应用程序提供的简单 online 的通讯簿，可用于通过 intranet 中发布的可搜索的目录。 通讯簿进行设计，以便用户可以请求有关员工的信息的一个或多个字段中输入搜索字符串。 若要显示远程数据服务的基本功能，示例应用程序有意保持较小，带有最少的对象和搜索字段。  
  
 应用程序接口由以下部分组成：  
  
-   非视觉**rds.DataControl**客户端用于连接到数据库的数据绑定对象。  
  
-   HTML 充当员工属性搜索条件的输入字段的文本框。  
  
-   HTML 命令按钮来生成查询，清除搜索字段、 包含员工信息更新数据库，取消挂起的更改，并导航的网格中显示的数据行。  
  
-   DHTML 数据绑定，使其显示数据从针对后端数据库的查询返回 (通过**rds.DataControl**数据绑定对象) 的表中。  
  
-   VBScript 连接每个前面提到的元素，并允许它们进行交互的例程。 VBScript 代码还用于初始化**rds.DataControl**对象，并动态创建 HTML 表的名称中的列标题**rds.DataControl**的字段记录集。  
  
 请从步骤使用链接到步骤以设置和运行方案并了解有关方案的工作方式的详细信息。  
  
 本方案包含以下主题。  
  
-   [通讯簿应用程序的系统要求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [运行通讯簿 SQL 脚本](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [运行通讯簿示例应用程序](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [通讯簿数据绑定对象](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [通讯簿命令按钮](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [通讯簿导航按钮](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>另请参阅  
 [通讯簿应用程序的系统要求](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX 数据对象 (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)



