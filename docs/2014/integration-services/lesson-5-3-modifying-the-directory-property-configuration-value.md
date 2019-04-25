---
title: 步骤 3：修改目录属性配置值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb83ac5bb1b811c23b782b01167c437e9b989518
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767359"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>步骤 3：修改目录属性配置值
  在此任务中，将针对包级变量 `User::varFolderName`的 Value 属性，修改存储在 SSISTutorial.dtsConfig 文件中的配置设置。 该变量可以更新 Foreach 循环容器的 Directory 属性。 修改后的值将指向`New Sample Data`你在上一任务中创建的文件夹。 修改了配置设置并运行包以后，该变量将使用从配置文件填充的值（而不是包中最初配置的目录值），来更新 Directory 属性。  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>修改目录属性的配置设置  
  
1.  在记事本或其他文本编辑器中，找到并打开在前一个任务中使用包配置向导创建的 SSISTutorial.dtsConfig 配置文件。  
  
2.  更改的值**ConfiguredValue**元素以匹配的路径`New Sample Data`你在上一任务中创建的文件夹。 请不要将路径用引号括起来。 如果`New Sample Data`文件夹是您的驱动器的根级别 (例如，c:\\)，则更新的 XML 应类似于下面的示例：  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     标题信息中， `GeneratedBy`， `GeneratedFromPackageID`，并**GeneratedDate**将不同在文件中，当然。 要注意的元素是 `Configuration` 元素。 变量 `Value` 的 `User::varFolderName` 属性现在包含 C:\New Sample Data。  
  
3.  保存更改，再关闭文本编辑器。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 4：测试第 5 课教程包](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
