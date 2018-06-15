---
title: 步骤 1： 配置 pymssql Python 开发环境 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a4a573ce609bfb5364a1dabac784eb760915b8a
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35309516"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>步骤 1： 配置 pymssql Python 开发的开发环境
你将需要配置你的开发环境满足先决条件，以便开发应用程序使用的 SQL Server Python 驱动程序。    
  
请注意，Python SQL 驱动程序使用 TDS 协议，默认情况下，SQL Server 和 Azure SQL 数据库中启用。  这种方式无需任何其他配置。  
  
## <a name="windows"></a>Windows  
  
1. **安装 Python 运行时和 pip 程序包管理器**  
A. 转到[python.org](https://www.python.org/downloads/)  
B. 单击相应的 Windows installer msi 链接。   
c. 一次下载的运行 msi 安装 Python 运行时  
  
2. **下载 pymssql 模块**从[此处](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    请确保选择正确的 whl 文件。  例如： 如果在 64 位计算机上使用 Python 2.7 选择： pymssql‑2.1.1‑cp27‑none‑win_amd64.whl。 一旦你下载.whl 文件将其放在 c: / Python27 文件夹。  
      
3. **打开 cmd.exe**  
  
4. **安装 pymssql 模块**     
    例如，如果你在使用 64 位计算机上使用 Python 2.7:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **安装 Python 运行时和 pip 程序包管理器**Python 在大多数的 Ubuntu 分发上可能已预安装。  如果您的计算机没有安装 python，你可以下载从源 tarball [python.org](https://www.python.org/downloads/)生成本地，或可以使用程序包管理器：  
```  
> sudo apt-get install python   
```  
  
2.  **打开终端**  
  
3.  **安装 pymssql 模块和依赖项**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **安装 Python 运行时和 pip 程序包管理器**  
A. 转到[python.org](https://www.python.org/downloads/)  
B. 单击相应的 Mac 安装程序 pkg 链接。   
c. 一次下载的运行 pkg 安装 Python 运行时  
  
2.  **打开终端**  
  
3. **安装 Homebrew 包管理器**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **安装 FreeTDS 模块**  
```  
> brew install FreeTDS  
```  
  
5.  **安装 pymssql 模块**  
```  
> sudo -H pip install pymssql  
```
