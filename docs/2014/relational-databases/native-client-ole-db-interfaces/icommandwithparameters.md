---
title: ICommandWithParameters |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c43b41faa03ae9838cc0dcec619179d272f238e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408147"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  以开头的数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 icommandwithparameters:: Getparameterinfo 若要获取的预期的结果更准确描述。 这些更准确的结果可能不同于 CommandWithParameters::GetParameterInfo 的早期版本中返回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
 此外从[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，在调用 icommandwithparameters:: Setparameterinfo，传递给的值时*pwszName*参数必须是有效的标识符。 有关详细信息，请参阅 [Database Identifiers](../databases/database-identifiers.md)。  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
