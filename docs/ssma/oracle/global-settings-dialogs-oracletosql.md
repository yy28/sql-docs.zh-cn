---
title: "全局设置 （对话框） (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43989355-cebf-4d8b-ba3d-fa8546e70230
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.workload: Inactive
ms.openlocfilehash: aa5f62dbde4489b17f2863fcbe1ebbf751e1198d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="global-settings-dialogs--oracletosql"></a>全局设置 （对话框） (OracleToSQL)
使用的对话框页**全局设置**对话框中指定的默认用户执行任何操作和 SSMA 警告设置。  
  
若要访问在该对话框设置**工具**菜单上，选择**全局设置**，单击**GUI**底部的左窗格中，，然后选择**对话框**。  
  
## <a name="options"></a>“常规”  
**覆盖对象之前，则发出警告**  
当 SSMA 将对象转换为 SQL Server 时，某些对象可能已经存在于项目的 SQL Server 元数据。 这些对象可能已转换，或对象可能只需具有在目标架构与要转换的对象相同的名称。  
  
使用此选项来指定是否 SSMA 应提示你输入覆盖重复的对象定义：  
  
-   如果你选择**True**，SSMA 将显示警告对话框中，当它遇到重复的对象。 在此对话框中，可以指定要重写单个对象或所有重复的对象，还是要跳过单个对象或所有重复的对象。  
  
-   如果你选择**False**、**对象覆盖默认操作**选项将显示你在其中指定的默认操作。  
  
**对象覆盖默认操作**  
如果选择，会显示此选项**False**为**覆盖对象之前发出警告**选项。  
  
使用此选项来指定默认对象覆盖行为：  
  
-   如果你选择**True**，SSMA 自动将覆盖具有相同的名称和要转换的对象相同的目标架构中的对象中的 SQL Server 项目元数据。  
  
-   如果你选择**False**，SSMA 在转换期间不会覆盖对象元数据。  
  
