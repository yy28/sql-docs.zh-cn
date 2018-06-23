---
title: ICommandWithParameters |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: edcba0cfc8ca284fd046f787829af4ba73dd366b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130104"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  以开头的数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 ICommandWithParameters::GetParameterInfo 以获取更准确的预期结果的说明。 这些更准确的结果可能与在以前版本的 CommandWithParameters::GetParameterInfo 返回的值不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
 此外从[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，当调用 ICommandWithParameters::SetParameterInfo，传递给值*pwszName*参数必须是有效的标识符。 有关详细信息，请参阅 [Database Identifiers](../databases/database-identifiers.md)。  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  