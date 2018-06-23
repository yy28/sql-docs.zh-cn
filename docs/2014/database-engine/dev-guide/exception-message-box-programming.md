---
title: 异常消息框中编程 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ExceptionMessageBox class, about ExceptionMessageBox class
- exception message box [SQL Server], about exception message box
- exception message box [SQL Server]
- interfaces [SQL Server]
- exceptions [SQL Server]
- messages [SQL Server], exception message box
ms.assetid: 0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0adef635d88a05925da924c4bab396f1da58e530
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026832"
---
# <a name="exception-message-box-programming"></a>异常消息框编程
  异常消息框是一个编程接口，与安装并且使用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]图形的组件。 异常消息框是支持的托管程序集，您可以将其用于应用程序中，以显著提高对消息传送的控制，并使用户可以选择保存错误消息内容，以供将来参考和从中获取有关消息的帮助。 由于异常消息框可由除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之外的所有 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 版本安装，因此在安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端组件的任何计算机上，无需额外配置即可使用该接口。  
  
 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 命名空间中的 <xref:Microsoft.SqlServer.MessageBox> 类除具有 <xref:System.Windows.Forms.MessageBox> 类的所有功能外，还具有一些其他功能。 对于可能使用 <xref:System.Windows.Forms.MessageBox> 的任何任务，<xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 均为理想之选，专用于很好地处理托管代码异常。 通过异常消息框，您可以执行以下操作：  
  
-   为多达五个按钮提供自定义按钮文本。 针对不同文本长度自动调整按钮和对话框的大小。  
  
-   允许用户将消息标题、文本、按钮文本和帮助链接（如果有）轻松复制到剪贴板上，或在电子邮件正文中轻松发送这些信息。  
  
-   当用户单击时在层次结构关系树中显示所有基础异常和错误**的其他信息**。  
  
-   允许用户决定当再次发生同一个异常时是否显示消息。  
  
-   使用与异常关联的帮助链接访问联机帮助系统。  
  
 有关详细信息，请参阅[异常消息框编程](../../../2014/database-engine/dev-guide/program-exception-message-box.md)。  
  
  