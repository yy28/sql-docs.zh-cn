---
title: 附录-1 （SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Appendix
ms.assetid: 6dcfd6d5-772c-4876-aa94-a7f43c4b9d59
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9d2d58b06c1a222a2ff6042bb5ca46338f752f7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083542"
---
# <a name="appendix---1-sybasetosql"></a>附录 - 1 (SybaseToSQL)
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
[执行 SSMA 控制台（Sybase）](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
