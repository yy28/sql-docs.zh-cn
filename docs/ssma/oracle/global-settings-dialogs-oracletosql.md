---
title: 全局设置 （对话框） (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 43989355-cebf-4d8b-ba3d-fa8546e70230
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.openlocfilehash: a85eb72b3c239b8be0141c445e5d4507efb438cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192340"
---
# <a name="global-settings-dialogs--oracletosql"></a>全局设置 （对话框） (OracleToSQL)
使用的对话框页面**全局设置**对话框可以指定的默认用户执行任何操作和 SSMA 的警告设置。  
  
若要访问该对话框设置在**工具**菜单中，选择**全局设置**，单击**GUI**在左窗格中，并选择底部**对话框**.  
  
## <a name="options"></a>选项  
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
  
