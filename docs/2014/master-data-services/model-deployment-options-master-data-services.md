---
title: 模型部署选项 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cf1b17b4-47d5-4eba-83f9-fb0555806867
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0dbc88c186e5f8f92c943c3e0d766ab6d8846941
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479027"
---
# <a name="model-deployment-options-master-data-services"></a>模型部署选项 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您部署某一模型包文件时，必须确定是部署新的或克隆的模型，还是更新以前已克隆的模型。  
  
## <a name="workflows"></a>工作流  
 当使用模型包时，有两个主要的工作流。  
  
-   在测试环境中创建某一模型的包以及将该模型的克隆部署到生产环境。 一段时间后，将来自测试环境的更新部署到生产环境。  
  
-   创建模型的包，然后将其作为新模型部署到相同的环境。 在此情况下，您必须为该模型提供一个新名称。  
  
## <a name="options"></a>选项  
 在 MDS 数据库中，每个模型对象都具有唯一的标识符 (ID)。 这些 ID 包含在模型部署包中。 在部署包时，您必须选择如何处理这些 ID。  
  
 下表可帮助您确定在使用系统管理模型部署向导或 MDSModelDeploy 工具时作出何种选择。  
  
|Option|Description|说明|  
|------------|-----------------|-----------|  
|新版|使用唯一名称创建一个新模型。 为所有模型对象创建新的标识符。|如果您使用新的标识符创建一个新模型，则在以后无法使用模型部署工具将更新应用于该模型。 在 Web 应用程序中使用向导部署一个模型包时，只有在具有相同名称或 ID 的模型已存在时，您才能选择创建一个新模型。|  
|克隆|创建一个新模型，该模型是包中模型的精确克隆。 这仅适用于该模型在目标环境中不存在的情况（按名称或标识符）。 如果想要在多个环境中拥有相同的模型并在经过一段时间后更新克隆的模型，请使用“克隆”。|这是 Web 应用程序中向导的默认行为。 如果已经存在具有相同名称或 ID 的模型，则系统将会提示您改为创建新的模型。|  
|Update|使用包中的模型更新现有模型。 标识符在这两个模型中必须相同。 这用来更新您以前克隆的模型。|您只能更新以前克隆的模型。 （名称和 ID 必须匹配。）|  
  
## <a name="see-also"></a>请参阅  
 [使用 MDSModelDeploy 部署模型部署包](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)   
 [使用向导部署模型部署包](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)   
 [部署模型 (Master Data Services)](deploying-models-master-data-services.md)  
  
  
