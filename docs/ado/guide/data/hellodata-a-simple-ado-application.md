---
title: HelloData：一个简单的 ADO 应用程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed92b3f83e865d2b8d4f3e3a3a3cb95e291d771e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63162093"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData：简单的 ADO 应用程序
此简单应用程序的四个主要的 ADO 操作每个步骤： 获取、 查看、 编辑和更新数据。 对 Microsoft® SQL Server 附带的 Northwind 示例数据库执行这些操作。 若要专注于 ADO 的基础知识并防止混乱代码，该示例中的错误处理很小。  
  
### <a name="to-run-hellodata"></a>若要运行 HelloData  
  
1.  创建引用 ADO 库的新标准 EXE Visual Basic 项目。 有关详细信息，请参阅[引用 ADO 库](../../../ado/guide/referencing-the-ado-libraries.md)。  
  
2.  在窗体，设置顶部创建四个命令按钮**名称**并**标题**属性设置为在本主题末尾的表中显示的值。  
  
3.  在按钮的下面添加**Microsoft DataGrid 控件**(Msdatgrd.ocx)。 Msdatgrd.ocx 文件包含使用 Visual Basic，位于 \windows\system32 或 \winnt\system32 目录中。 若要将 DataGrid 控件添加到 Visual Basic 工具箱窗格中，选择**组件...** 从**项目**菜单。 然后旁边的复选框"Microsoft DataGrid 控件 6.0 (SP3) (OLEDB)"，然后单击**确定**。 要将控件添加到项目中，将 DataGrid 控件从工具箱拖动到 Visual Basic 窗体。  
  
4.  创建**文本框中**网格下窗体上并设置其属性表中所示。 完成后，窗体应类似于下图。  
  
5.  最后，将复制中列出的代码[HelloData 代码](../../../ado/guide/data/hellodata-code.md)，并将其粘贴到窗体的代码编辑器窗口。 按**F5**要运行此代码。  
  
> [!NOTE]
>  在以下示例中，并在整个指南，用于对服务器进行身份验证的用户 id"MyId"使用密码的"123aBc"。 为您的服务器，应将这些值与有效的登录凭据。 此外，替换为你的服务器的名称的"MySQLServer"值。  
  
 有关代码的详细说明，请参阅[对 HelloData 的注释](../../../ado/guide/data/comments-on-hellodata.md)。  
  
 ![显示 HelloData VB 应用程序的 Form1](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|控件类型|属性|值|  
|------------------|--------------|-----------|  
|Form|“属性”|Form1|  
||高度|6500|  
||宽度|6500|  
|MS DataGrid|“属性”|grdDisplay1|  
|TextBox|“属性”|txtDisplay1|  
||多行|true|  
|命令按钮|“属性”|cmdGetData|  
||Caption|获取数据|  
|命令按钮|“属性”|cmdExamineData|  
||Caption|检查数据|  
|命令按钮|“属性”|cmdEditData|  
||Caption|编辑数据|  
|命令按钮|“属性”|cmdUpdateData|  
||Caption|更新数据|
