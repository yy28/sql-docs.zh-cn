---
title: 附录-1 （DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c6a30367-d56f-4fcc-8920-c6a6b0335a67
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 70d916526f5b7d7d36c9237624ef311befca39c1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938351"
---
# <a name="appendix---1-db2tosql"></a>附录1（DB2ToSQL）
SSMA 控制台命令行选项的快速视图：  
  
|Sl. 不是。|开关|是否必需？|开关参数|允许的值|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/脚本|是|scriptfile|有效的 XML 文件名。<br /><br />控制台脚本定义文件。|  
|2|-v/variable|否|variablevaluefile|有效的 XML 文件名。<br /><br />如果脚本文件中使用了变量，则必须指定此文件。|  
|3|-c/microsoft.sqlserver.management.common.serverconnection>|否|serverconnectionfile|有效的 XML 文件名。<br /><br />此文件包含服务器连接信息。|  
|4|-x/xmloutput|否|xmloutputfile|此选项表示 XML 格式的控制台输出。 如果未指定此选项，则默认输出为文本格式。<br /><br />如果未指定 xmloutputfile，则将 XML 输出定向到 STDOUT。<br /><br />Xmloutputfile 是以 XML 格式写入控制台输出的文件的名称。|  
|5|-l/log|否|logfile|有效的文件名。|  
|6|-e/projectenvironment|否|projectenvironmentfolder|包含 SSMA 项目环境文件的有效文件夹名称。|  
|7|-p/securepassword|否|-a/add {<server_id> [,.。。n] &#124; all}-c&#124;microsoft.sqlserver.management.common.serverconnection> <服务器-连接文件> [-v&#124;变量 <变量值文件>] [-o/overwrite]<br /><br />或<br /><br />-a/add {<server_id> [,.。。n] &#124; 所有}-s&#124;脚本 <脚本文件> [-v&#124;变量 <变量值文件>] [-o/overwrite]<br /><br />-r/remove {<server_id> [，.。。n] &#124;<br /><br />-l/list<br /><br />-e/export {<服务器 id> [，.。。n] &#124; all} <加密-密码文件><br /><br />-i/import {<服务器 id> [，.。。n] &#124; all} <加密-密码文件>|如果指定此选项，则不能与其他任何选项组合。<br /><br />服务器 id：为服务器 {string} 提供的唯一 ID<br /><br />服务器连接文件：服务器定义文件（serverconnectionfile 或 scriptfile）。<br /><br />变量-值文件：它是一个变量定义文件，并在服务器连接文件中使用。<br /><br />加密密码-文件：它是使用用户指定的密码加密的服务器密码文件。|  
|8|-?|否|不适用|不适用|  
  
## <a name="see-also"></a>另请参阅  
[执行 SSMA 控制台](https://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
