---
title: "重新部署包 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "重新部署包 [Integration Services]"
  - "部署包 [Integration Services], 重新部署"
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# 重新部署包
  在部署项目后，您可能需要更新或扩展包功能，然后重新部署包含更新包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。 在重新部署包的过程中，您应该检查部署实用工具中包括的配置属性。 例如，您可能不希望在重新部署包后允许对配置进行更改。  
  
## 重新部署过程  
 在完成更新包后，您应该重新生成该项目，将部署文件夹复制到目标计算机，然后重新运行包安装向导。  
  
 如果只更新项目中的少数几个包，您可能不希望重新部署整个项目。 若要仅部署几个包，可以新建一个 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目，将更新后的包添加到新的项目，然后生成并部署该项目。 在将包添加到其他项目时，包配置会自动随包一起复制。  
  
## 相关任务  
 [使用部署实用工具部署包](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)  
  
  