---
title: 步骤 3：修改目录属性配置值 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a71a7a181322d60caca98da4ddf3261cbce99c9e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440364"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>步骤 3：修改目录属性配置值
  在此任务中，将针对包级变量 `User::varFolderName`的 Value 属性，修改存储在 SSISTutorial.dtsConfig 文件中的配置设置。 该变量可以更新 Foreach 循环容器的 Directory 属性。 修改后的值将指向在 `New Sample Data` 上一任务中创建的文件夹。 修改了配置设置并运行包以后，该变量将使用从配置文件填充的值（而不是包中最初配置的目录值），来更新 Directory 属性。  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>修改目录属性的配置设置  
  
1.  在记事本或其他文本编辑器中，找到并打开在前一个任务中使用包配置向导创建的 SSISTutorial.dtsConfig 配置文件。  
  
2.  更改**ConfiguredValue**元素的值，使其与 `New Sample Data` 在上一任务中创建的文件夹的路径匹配。 请不要将路径用引号括起来。 如果 `New Sample Data` 文件夹在驱动器的根级别（例如，C： \\ ），则更新的 XML 应类似于以下示例：  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     当然，标题信息、、 `GeneratedBy` `GeneratedFromPackageID` 和**GeneratedDate**在文件中将有所不同。 要注意的元素是 `Configuration` 元素。 变量 `Value` 的 `User::varFolderName` 属性现在包含 C:\New Sample Data。  
  
3.  保存更改，再关闭文本编辑器。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 4：测试第 5 课教程包](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
