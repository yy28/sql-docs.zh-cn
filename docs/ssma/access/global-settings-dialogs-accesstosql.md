---
title: 全局设置 （对话框） (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6c2204f2-d49e-49ba-9c0f-f14cf07fa561
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dd1068e509a14c9d7388beea3727f2b30dd3ba40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299271"
---
# <a name="global-settings-dialogs-accesstosql"></a>全局设置 （对话框） (AccessToSQL)
使用的对话框页面**全局设置**对话框可以指定的默认用户执行任何操作和 SSMA 的警告设置。  
  
若要访问该对话框设置在**工具**菜单中，选择**全局设置**，单击**GUI**在左窗格中，并选择底部**对话框**.  
  
## <a name="options"></a>选项  
**在启动时显示迁移向导**  
SSMA for Access 中, 你可以选择启用或禁用**迁移向导**SSMA 应用程序启动。 默认情况下，此选项才 **，则返回 True**。  
  
-   如果该选项设置为 **，则返回 True**，迁移向导显示此对话框最初打开 SSMA 访问应用程序。  
  
-   如果该选项设置为**False**，迁移向导不会显示并且将必须手动访问从**文件**必要的菜单。  
  
**覆盖对象之前，则发出警告**  
当 SSMA 将对象转换为 SQL Server 时，一些对象可能已存在于项目的 SQL Server 元数据。 这些对象可能已经转换，或对象可能只是必须在目标架构中与要转换的对象相同的名称。  
  
使用此选项以指定是否 SSMA 应提示你覆盖重复的对象定义：  
  
-   如果选择 **，则返回 True**，SSMA 遇到一个复制对象时将显示一个警告对话框。 在此对话框中，可以指定覆盖单个对象或所有重复的对象，或跳过单个对象或所有重复的对象。  
  
-   如果选择**False**，则**对象覆盖默认操作**选项将显示在其中指定的默认操作。  
  
**对象覆盖默认操作**  
如果您选择，将显示此选项**False**有关**覆盖对象之前给出警告**选项。  
  
使用此选项指定的默认对象覆盖行为：  
  
-   如果选择 **，则返回 True**，SSMA 会自动覆盖具有相同的名称和要转换的对象相同的目标架构中的对象中的 SQL Server 项目元数据。  
  
-   如果选择**False**，SSMA 在转换期间不会覆盖对象元数据。  
  
