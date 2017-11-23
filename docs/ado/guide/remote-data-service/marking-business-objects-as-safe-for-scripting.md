---
title: "将标记为可安全执行脚本的业务对象 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45f9656022a71deab0cb91a3d9667cbd314c2ffb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>将标记为可安全执行脚本的业务对象
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要帮助确保安全的 Internet 环境，你需要将实例化的任何业务对象标记[rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)对象的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法为"安全执行脚本。" 你需要确保它们标记这种情况下在系统注册表的许可证区域后，才可以使用 DCOM。  
  
> [!NOTE]
>  可以实例化和初始化的任何人都通过网络标记为"可安全执行脚本"或可安全执行初始化的业务对象。 将业务对象标记为"可安全执行脚本"不作其安全。 它是非常重要，若要确保使用最高的安全性，以确保此类对象不会存在敏感数据的未受保护的访问点编码的业务对象。  
  
 要手动将标记为可安全执行脚本业务对象，创建包含以下文本的扩展名为.reg 文本文件。 在此示例中， \< *MyActiveXGUID*> 是业务对象的十六进制 GUID 数。 以下两个数字启用安全的脚本功能：  
  
```  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 保存文件并将其合并到您的注册表中，通过使用注册表编辑器或双击 Windows 资源管理器中的.reg 文件。  
  
 创建在 Microsoft Visual Basic 中的业务对象可以自动标记为"可安全执行脚本"，与包和部署向导。 当向导要求您指定的安全设置时，选择**安全的初始化**和**可安全执行脚本**。  
  
 在最后一个步骤中，应用程序安装程序向导创建一个.htm 文件和.cab 文件。 然后可以将这两个文件复制到目标计算机，并双击要加载页，并正确注册服务器的.htm 文件。  
  
 因为默认情况下，将在 Windows\System32\Occache 目录中安装的业务对象，将其移到 Windows\System32 目录和更改**HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32**注册表项以匹配的正确路径。


