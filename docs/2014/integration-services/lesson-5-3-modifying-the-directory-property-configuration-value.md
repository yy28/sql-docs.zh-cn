---
title: 步骤 3：修改目录属性配置值 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
caps.latest.revision: 29
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f9e1be6c1c9fc9abb12716cda9ba244d8ce5427b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124807"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>步骤 3：修改目录属性配置值
  在此任务中，将针对包级变量 `User::varFolderName` 的 Value 属性，修改存储在 SSISTutorial.dtsConfig 文件中的配置设置。 该变量可以更新 Foreach 循环容器的 Directory 属性。 修改后的值将指向`New Sample Data`你在上一任务中创建的文件夹。 修改了配置设置并运行包以后，该变量将使用从配置文件填充的值（而不是包中最初配置的目录值），来更新 Directory 属性。  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>修改目录属性的配置设置  
  
1.  在记事本或其他文本编辑器中，找到并打开在前一个任务中使用包配置向导创建的 SSISTutorial.dtsConfig 配置文件。  
  
2.  更改的值**ConfiguredValue**元素以匹配的路径`New Sample Data`你在上一任务中创建的文件夹。 请不要将路径用引号括起来。 如果`New Sample Data`文件夹是你的驱动器的根级别 (例如，c:\\)，更新的 XML 应类似于下面的示例：  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     标题信息中， `GeneratedBy`， `GeneratedFromPackageID`，和**GeneratedDate**将不同在文件中，这是当然的。 要注意的元素是 `Configuration` 元素。 变量 `User::varFolderName` 的 `Value` 属性现在包含 C:\New Sample Data。  
  
3.  保存更改，再关闭文本编辑器。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 4：测试第 5 课教程包](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  