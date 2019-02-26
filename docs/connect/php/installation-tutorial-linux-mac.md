---
title: Linux 和 macOS 的 Microsoft Drivers for PHP for SQL Server 安装教程 |Microsoft Docs
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: a31b17b8fbe2130b84b27be08d1a6218d697f9f2
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744627"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux 和 macOS 的 Microsoft Drivers for PHP for SQL Server 安装教程
以下说明假定干净的环境，并显示如何安装 PHP 7.x、 Microsoft ODBC 驱动程序、 Apache 和 Microsoft Drivers for PHP for SQL Server 在 Ubuntu 16.04、 18.04 和 18.10，RedHat 7，Debian 8 和 9，Suse 12 月 15 日和 macOS 10.1210.13 和 10.14。 这些说明建议安装驱动程序使用 PECL，但你也可以下载预生成二进制文件[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 项目页，然后安装它们中的说明[Microsoft Drivers for PHP 加载适用于 SQL Server](../../connect/php/loading-the-php-sql-driver.md)。 扩展加载和我们为什么不添加到 php.ini 下扩展的说明，请参阅的部分上[加载的驱动程序](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup)。

默认情况下，这些说明安装 PHP 7.3。 请注意，某些支持 Linux 发行版默认为 PHP 7.0 或更低，SQL Server--不支持的 PHP 驱动程序，请参阅每个部分，若要改为安装 PHP 7.1 或 7.2 开头处的说明。

## <a name="contents-of-this-page"></a>此页的内容：

- [在 Ubuntu 16.04、 18.04 和 18.10 上安装驱动程序](#installing-the-drivers-on-ubuntu-1604-1804-and-1810)
- [Red Hat 7 上安装驱动程序](#installing-the-drivers-on-red-hat-7)
- [在 Debian 8 和 9 上安装驱动程序](#installing-the-drivers-on-debian-8-and-9)
- [在 Suse 12 和 15 上安装驱动程序](#installing-the-drivers-on-suse-12-and-15)
- [MacOS Sierra、 High Sierra 和 Mojave 上安装驱动程序](#installing-the-drivers-on-macos-sierra-high-sierra-and-mojave)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-1810"></a>在 Ubuntu 16.04、 18.04 和 18.10 上安装驱动程序

> [!NOTE]
> 若要安装 PHP 7.1 或 7.2，替换为 7.3 7.1 或 7.2 中的以下命令。

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.3 php7.3-dev php7.3-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>步骤 2. 安装先决条件
Ubuntu 按照的说明安装的 ODBC 驱动程序[Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装用于 Microsoft SQL Server PHP 驱动程序
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步骤 4. 安装 Apache 和配置驱动程序加载
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/20-sqlsrv.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重启 Apache 并测试的示例脚本
```
sudo service apache2 restart
```
若要测试您的安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="installing-the-drivers-on-red-hat-7"></a>Red Hat 7 上安装驱动程序

> [!NOTE]
> 若要安装 PHP 7.1 或 7.2，替换为 remi php73 remi php71 或 remi php72 分别在以下命令。

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php73
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>步骤 2. 安装先决条件
Red Hat 7 的说明安装的 ODBC 驱动程序[Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

编译与 PHP 7.2 或 7.3 PECL 的 PHP 驱动程序需要较新的 gcc 高级版，而不是默认：
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装用于 Microsoft SQL Server PHP 驱动程序
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
即使你已升级 GCC PECL 中的一个问题可能会阻止最新版本的驱动程序的正确的安装。 若要安装、 下载的程序包和手动编译 （类似的步骤以 pdo_sqlsrv）：
```
pecl download sqlsrv
tar xvzf sqlsrv-5.6.0.tgz
cd sqlsrv-5.6.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
或者可以下载预生成二进制文件[Github 项目页](https://github.com/Microsoft/msphpsql/releases)，或从 Remi 存储库安装：
```
sudo yum install php-sqlsrv
```
### <a name="step-4-install-apache"></a>步骤 4. 安装 Apache
```
sudo yum install httpd
```
SELinux 会默认安装，并在强制模式下运行。 若要允许 Apache SELinux 通过连接到数据库，请运行以下命令：
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重启 Apache 并测试的示例脚本
```
sudo apachectl restart
```
若要测试您的安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="installing-the-drivers-on-debian-8-and-9"></a>在 Debian 8 和 9 上安装驱动程序

> [!NOTE]
> 若要安装 PHP 7.1 或 7.2，替换为以下命令中的 7.3 7.1 或 7.2。

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.3 php7.3-dev php7.3-xml
```
### <a name="step-2-install-prerequisites"></a>步骤 2. 安装先决条件
Debian 按照的说明安装的 ODBC 驱动程序[Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

您可能还需要生成正确的区域设置获取 PHP 输出，以在浏览器中正确显示。 例如，对于 en_US utf-8 区域设置，运行以下命令：
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装用于 Microsoft SQL Server PHP 驱动程序
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步骤 4. 安装 Apache 和配置驱动程序加载
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/20-sqlsrv.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重启 Apache 并测试的示例脚本
```
sudo service apache2 restart
```
若要测试您的安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="installing-the-drivers-on-suse-12-and-15"></a>在 Suse 12 和 15 上安装驱动程序

> [!NOTE]
> 在下面的说明，将为<SuseVersion>与版本的 Suse-如果你使用的 Suse Enterprise Linux 15，它是 SLE_15 或 SLE_15_SP1，并同样对于其他版本。 并非所有版本的 PHP 都了可用于所有版本的 Suse Linux-请都参阅`http://download.opensuse.org/repositories/devel:/languages:/php`若要查看哪些版本的 Suse 具有默认版本可用，PHP 或`http://download.opensuse.org/repositories/devel:/languages:/php:/`查看哪些其他版本的 PHP 都可 Suse 的各个版本。

> [!NOTE]
> PHP 7.3 的包不可用于 Suse 12。 若要安装 PHP 7.1，下面的存储库 URL 将替换为以下 URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php71/<SuseVersion>/devel:languages:php:php71.repo`。
> 若要安装 PHP 7.2，下面的存储库 URL 将替换为以下 URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`。

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>步骤 2. 安装先决条件
Suse 的说明安装的 ODBC 驱动程序[Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装用于 Microsoft SQL Server PHP 驱动程序
> [!NOTE]
> 如果收到错误消息：`Connection to 'pecl.php.net:443' failed: Unable to find the socket transport "ssl"`中，编辑在 /usr/bin/pecl pecl 脚本并删除`-n`切换最后一行中。 此参数可防止 PECL 调用 PHP 时，这样可防止加载 OpenSSL 扩展加载 ini 文件。

```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步骤 4. 安装 Apache 和配置驱动程序加载
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重启 Apache 并测试的示例脚本
```
sudo systemctl restart apache2
```
若要测试您的安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="installing-the-drivers-on-macos-sierra-high-sierra-and-mojave"></a>MacOS Sierra、 High Sierra 和 Mojave 上安装驱动程序

如果你还没有它，安装 brew，如下所示：
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> 若要安装 PHP 7.1 或 7.2，替换php@7.3与php@7.1或php@7.2分别在以下命令。

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP

```
brew tap
brew tap homebrew/core
brew install php@7.3
```
PHP 现在应在你的路径-运行`php -v`以验证你是否正在运行的 PHP 的正确版本。 如果在你的路径不是 PHP 或不正确的版本，运行以下命令：
```
brew link --force --overwrite php@7.3
```

### <a name="step-2-install-prerequisites"></a>步骤 2. 安装先决条件
通过以下上的说明安装适用于 macOS 的 ODBC 驱动程序[Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

此外，您可能需要安装 GNU 使工具：
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装用于 Microsoft SQL Server PHP 驱动程序
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步骤 4. 安装 Apache 和配置驱动程序加载
```
brew install apache2
```
若要查找 Apache Apache 安装的配置文件，请运行 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
并将其替换为路径`httpd.conf`在以下命令：
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重启 Apache 并测试的示例脚本
```
sudo apachectl restart
```
若要测试您的安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="testing-your-installation"></a>测试安装

若要测试此示例脚本，创建名为 testsql.php 系统的文档根目录中的文件。 这是`/var/www/html/`在 Ubuntu、 Debian 以及 Redhat`/srv/www/htdocs`上 SUSE 或`/usr/local/var/www`在 macOS 上。 将以下脚本复制到其中，替换服务器、 数据库、 用户名和密码作为适当。
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

// Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if ($conn === false) {
    die(formatErrors(sqlsrv_errors()));
}

// Select Query
$tsql = "SELECT @@Version AS SQL_VERSION";

// Executes the query
$stmt = sqlsrv_query($conn, $tsql);

// Error handling
if ($stmt === false) {
    die(formatErrors(sqlsrv_errors()));
}
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```
将浏览器指向 https://localhost/testsql.php(https://localhost:8080/testsql.php在 macOS 上)。 现在应能够连接到你的 SQL Server/Azure SQL 数据库。

## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[加载 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 系统要求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
