---
title: 附录-1 (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Appendix
ms.assetid: 6dcfd6d5-772c-4876-aa94-a7f43c4b9d59
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 184ee95eaa82002813ee37492da0f6193730567e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="appendix---1-sybasetosql"></a>附录-1 (SybaseToSQL)
SSMA 控制台命令行选项的快速视图：  
  
|Sl。 否。|开关|必需？|开关参数|允许的值|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|是|scriptfile|有效的 XML 文件名称。<br /><br />控制台脚本定义文件。|  
|2|-v/变量|否|variablevaluefile|有效的 XML 文件名称。<br /><br />如果脚本文件中使用变量，则必须指定此文件。|  
|3|-c/serverconnection|否|serverconnectionfile|有效的 XML 文件名称。<br /><br />此文件包含服务器连接信息。|  
|4|-x/xmloutput|否|xmloutputfile|此选项指示以 XML 格式的控制台输出。 如果未指定此选项，默认输出是以文本格式。<br /><br />如果未指定 xmloutputfile，XML 输出定向到 STDOUT。<br /><br />Xmloutputfile 是文件的向其写入控制台输出以 XML 格式的名称。|  
|5|-l/日志|否|logfile|有效的文件名称。|  
|6|-e/projectenvironment|否|projectenvironmentfolder|有效的文件夹名称包含 SSMA 项目环境文件。|  
|7|-p/securepassword|否|-a/添加 {< server_id > [，… n]&#124;所有} – c&#124;serverconnection < 服务器连接文件 > [-v&#124;变量 < 变量值文件 >] [-o/覆盖]<br /><br />或<br /><br />-a/添加 {< server_id > [，… n]&#124;所有} – s&#124;脚本 < 脚本文件 > [-v&#124;变量 < 变量值文件 >] [-o/覆盖]<br /><br />-r/删除 {< server_id > [，… n]&#124;所有}<br /><br />-l/列表<br /><br />– e/导出 {< 服务器 id > [，… n]&#124;所有} < 加密的密码-文件 ><br /><br />– i / 导入 {< 服务器 id > [，… n]&#124;所有} < 加密密码的文件 >|如果指定，此选项必须不能与任何其他选项结合。<br /><br />服务器 id： 为 {字符串} 的服务器提供唯一的 ID<br /><br />服务器连接文件： 服务器定义文件 （serverconnectionfile 或脚本文件）。<br /><br />变量值文件： 它是变量定义文件，并用于服务器连接文件。<br /><br />加密密码 – 文件： 它是使用用户指定通行短语加密 server 密码文件。|  
|8|-?|否|不适用|不适用|  
  
## <a name="see-also"></a>另请参阅  
[执行 SSMA 控制台 (Sybase)](http://msdn.microsoft.com/en-us/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
