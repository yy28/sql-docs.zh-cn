---
title: 将标记为对于脚本化的业务对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 18f14920ae532e344ddb69ee79fdc0bd838af95b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699473"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>将业务对象标记为“可安全编写脚本”
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要帮助确保环境安全的 Internet，需要将任何业务对象使用实例化标记[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)对象的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法为"安全执行脚本。" 您需要确保它们标记这种情况下在系统注册表的许可区域才可以在 DCOM 中使用。  
  
> [!NOTE]
>  可以实例化并初始化任何人都在网络上标记为"可安全执行脚本"或安全初始化的业务对象。 将业务对象标记为"安全执行脚本编写"不会使其安全。 它是极其重要，以确保业务对象进行编码以最高的安全性，以确保此类对象不会显示敏感数据的未受保护的访问点。  
  
 若要手动将标记为对于脚本化业务对象，创建包含以下文本的扩展名为.reg 文本文件。 在此示例中， \< *MyActiveXGUID*> 是您的业务对象的十六进制 GUID 编号。 以下两个数字启用安全的脚本功能：  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 保存该文件并将其合并到注册表中，通过使用注册表编辑器或通过双击 Windows 资源管理器中的.reg 文件。  
  
 创建 Microsoft Visual Basic 中的业务对象可以自动标记为"可安全执行脚本"使用包和部署向导。 当向导要求您指定的安全设置时，选择**安全初始化**并**安全执行脚本编写**。  
  
 在最后一个步骤中，应用程序安装程序向导创建一个.htm 文件和一个.cab 文件。 然后可以将这两个文件复制到目标计算机，并双击要加载页，并正确注册服务器的.htm 文件。  
  
 由于默认情况下，将在 Windows\System32\Occache 目录中安装的业务对象，将其移动到 Windows\System32 目录并将更改**HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32**注册表项以匹配正确的路径。


