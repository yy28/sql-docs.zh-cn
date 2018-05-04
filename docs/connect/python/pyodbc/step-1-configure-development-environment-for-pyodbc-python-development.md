---
title: 步骤 1： 配置 pyodbc Python 开发环境 |Microsoft 文档
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: beb0c34f5645615a69944088163ad157d59d3c3a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>步骤 1： 配置 pyodbc Python 开发的开发环境

## <a name="windows"></a>Windows  
通过使用 Python-在 Windows 上的 pyodbc 连接到 SQL 数据库：
  
1. **下载 Python 安装程序**  
  如果您的计算机不具有 Python 请安装它。 请转到[Python 下载页](https://www.python.org/downloads/windows/)并下载适当的安装程序。 例如，如果您是在 64 位计算机上，下载 Python 2.7 或 3.5 (x64) 安装程序。  
  
2. **安装 Python**安装在下载之后，执行以下操作：。 双击文件以启动安装程序。 b. 选择你的语言，并同意这些条款。 c. 按照屏幕上的说明和 Python 应安装在你的计算机上。 d. 可以通过转到 C:\Python27 或 C:\Python35 安装了 Python，运行 python-v 或 py v （针对 3.x)，它是验证 
      
3. [**安装 Microsoft ODBC 驱动程序**](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)
  
4. **以管理员身份打开 cmd.exe**     

5. **安装 Python 包管理器的 pyodbc 使用 pip-**
```  
> cd C:\Python27\Scripts>  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
通过使用 Python-pyodbc Ubuntu 和 RedHat 上连接到 SQL 数据库：
  
1. **打开终端**  

2. **安装适用于 Linux 的 Microsoft ODBC Driver 13**适用于 Ubuntu 15.04 + 
``` 
> sudo su  
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-Ubuntu-b87369f0/file/154097/2/installodbc.sh  
> sh installodbc.sh  
```   

  对于 RedHat 6，7 
``` 
> sudo su 
> wget https://gallery.technet.microsoft.com/ODBC-Driver-13-for-SQL-8d067754/file/153653/4/install.sh 
> sh install.sh 
```  
  
3.  **安装 pyodbc**  
```  
> sudo -H pip install pyodbc
```
