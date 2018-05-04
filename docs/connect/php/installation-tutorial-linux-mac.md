---
title: Linux 和 macOS Microsoft Drivers for PHP for SQL Server 的安装教程 |Microsoft 文档
ms.date: 04/11/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: c9a28604fb55c81c4fcca0df542110d6347f3ee5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux 和 macOS Microsoft Drivers for PHP for SQL Server 的安装教程
以下说明假定一个干净的环境，并演示如何以 PHP 7.x、 Microsoft ODBC 驱动程序、 Apache 和 Microsoft 驱动程序安装 SQL Server 上 Ubuntu 16.04 和 17.10，RedHat 7、 8 和 9，Suse 12 Debian，和 macOS X 10.11 和 10.12 for PHP。 这些说明建议安装驱动程序使用 PECL，但你也可以下载的预构建的二进制文件从[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 项目页，并将其中的说明安装[加载 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)。 有关扩展加载和为何我们不希望向 php.ini 添加扩展的说明，请参阅部分[加载驱动程序](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup)。

默认情况下 — 这些指令安装 PHP 7.2 参阅每个部分，若要安装 PHP 7.0 或 7.1 开头的说明。

## <a name="contents-of-this-page"></a>此页的内容：

- [在 Ubuntu 16.04 和 17.10 上安装驱动程序](#installing-the-drivers-on-ubuntu-1604-and-1710)
- [在 Red Hat 7 上安装驱动程序](#installing-the-drivers-on-red-hat-7)
- [在 Debian 8 和 9 上安装驱动程序](#installing-the-drivers-on-debian-8-and-9)
- [在 Suse 12 上安装驱动程序](#installing-the-drivers-on-suse-12)
- [在 macOS El Capitan 和 Sierra 上安装驱动程序](#installing-the-drivers-on-macos-el-capitan-and-sierra)

## <a name="installing-the-drivers-on-ubuntu-1604-and-1710"></a>在 Ubuntu 16.04 和 17.10 上安装驱动程序

> [!NOTE]
> 若要安装 PHP 7.0 或 7.1，将替换为 7.0 或以下命令中的 7.1 7.2。

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.2 php7.2-dev php7.2-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>步骤 2. 安装必备组件
Ubuntu 的说明安装的 ODBC 驱动程序[Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装 Microsoft SQL Server PHP 驱动程序
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步骤 4. 安装 Apache 和配置驱动程序加载
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重新启动 Apache 并测试的示例脚本
```
sudo service apache2 restart
```
若要测试安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="installing-the-drivers-on-red-hat-7"></a>在 Red Hat 7 上安装驱动程序

> [!NOTE]
> 若要安装 PHP 7.0 或 7.1，替换 remi php72 remi php70 或 remi-php71 分别在以下命令。

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php72
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>步骤 2. 安装必备组件
Red Hat 7 的说明安装的 ODBC 驱动程序[Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

编译的 PHP 驱动程序与使用 PHP 7.2 PECL 需要而不是默认最近 GCC:
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装 Microsoft SQL Server PHP 驱动程序
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
即使你已升级 GCC PECL 中的问题可能会阻止驱动程序的最新版本的正确安装。 若要安装，请下载包并手动编译：
```
pecl download sqlsrv
tar xvzf sqlsrv-5.2.0.tgz
cd sqlsrv-5.2.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
或者，你可以下载的预构建的二进制文件从[Github 项目页](https://github.com/Microsoft/msphpsql/releases)，或从 Remi 存储库安装：
```
sudo yum install php-sqlsrv php-pdo_sqlsrv
```
### <a name="step-4-install-apache"></a>步骤 4. 安装 Apache
```
sudo yum install httpd
```
SELinux 默认情况下安装，并在强制模式下运行。 若要允许 Apache SELinux 通过连接到数据库，运行以下命令：
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重新启动 Apache 并测试的示例脚本
```
sudo apachectl restart
```
若要测试安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="installing-the-drivers-on-debian-8-and-9"></a>在 Debian 8 和 9 上安装驱动程序

> [!NOTE]
> 若要安装 PHP 7.0 或 7.1，将替换为 7.0 或 7.1 7.2 以下命令中。

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install –y php7.2 php7.2-dev php7.2-xml
```
### <a name="step-2-install-prerequisites"></a>步骤 2. 安装必备组件
Debian 的说明安装的 ODBC 驱动程序[Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

你可能还需要生成正确的区域设置，若要获取 PHP 输出以在浏览器中正确显示。 例如，对于 en_US utf-8 区域设置时，运行以下命令：
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装 Microsoft SQL Server PHP 驱动程序
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步骤 4. 安装 Apache 和配置驱动程序加载
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重新启动 Apache 并测试的示例脚本
```
sudo service apache2 restart
```
若要测试安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="installing-the-drivers-on-suse-12"></a>在 Suse 12 上安装驱动程序

> [!NOTE]
> 若要安装 PHP 7.0，跳过以下命令添加存储库-7.0 是 suse 12 上的默认值 PHP。
> 若要安装 PHP 7.1，请将下面的存储库 URL 替换以下 URL: `http://download.opensuse.org/repositories/devel:/languages:/php:/php71/SLE_12/devel:languages:php:php71.repo`

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP
```
sudo su
zypper -n ar -f http://download.opensuse.org/repositories/devel:languages:php/SLE_12/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel
```
### <a name="step-2-install-prerequisites"></a>步骤 2. 安装必备组件
Suse 12 的说明在上安装的 ODBC 驱动程序[Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装 Microsoft SQL Server PHP 驱动程序
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步骤 4. 安装 Apache 和配置驱动程序加载
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重新启动 Apache 并测试的示例脚本
```
sudo systemctl restart apache2
```
若要测试安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="installing-the-drivers-on-macos-el-capitan-and-sierra"></a>在 macOS El Capitan 和 Sierra 上安装驱动程序

如果你还没有它，安装酿造，如下所示：
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> 若要安装 PHP 7.0 或 7.1，替换php@7.2与php@7.0或php@7.1分别在以下命令。

### <a name="step-1-install-php"></a>步骤 1. 安装 PHP

```
brew tap
brew tap homebrew/core
brew install php@7.2
```
PHP 现在应在你的路径-运行`php -v`以验证你是否正在运行的 PHP 的正确版本。 如果 PHP 不在你的路径或不是正确的版本，运行以下命令：
```
brew link --force --overwrite php@7.2
```

### <a name="step-2-install-prerequisites"></a>步骤 2. 安装必备组件
按照的说明安装的 ODBC driver for macOS [Linux 和 macOS 安装页](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。 

此外，你可能需要安装 GNU 生成工具：
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>步骤 3. 安装 Microsoft SQL Server PHP 驱动程序
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>步骤 4. 安装 Apache 和配置驱动程序加载
```
brew install apache2
```
若要查找 Apache Apache 安装的配置文件，运行 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
和用来替换路径`httpd.conf`中的以下命令：
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>步骤 5. 重新启动 Apache 并测试的示例脚本
```
sudo apachectl restart
```
若要测试安装，请参阅[测试安装](#testing-your-installation)本文档末尾。

## <a name="testing-your-installation"></a>测试安装

若要测试此示例脚本，创建在您的系统的文档根节点名 testsql.php 的文件。 这是`/var/www/html/`上 Ubuntu、 Debian 和 Redhat，`/srv/www/htdocs`上 SUSE，或`/usr/local/var/www`在 macOS 上。 将以下脚本复制到其中，替换服务器、 数据库、 用户名和密码作为适当。
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "Database" => "yourDatabase",
    "Uid" => "yourUsername",
    "PWD" => "yourPassword"
);

//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if( $conn === false ) {
    die( FormatErrors( sqlsrv_errors()));
}

//Select Query
$tsql= "SELECT @@Version as SQL_VERSION";

//Executes the query
$getResults= sqlsrv_query($conn, $tsql);

//Error handling
if ($getResults == FALSE)
    die(FormatErrors(sqlsrv_errors()));
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['SQL_VERSION']);
    echo ("<br/>");
}

sqlsrv_free_stmt($getResults);

function FormatErrors( $errors )
{
    /* Display errors. */
    echo "Error information: <br/>";
    foreach ( $errors as $error )
    {
        echo "SQLSTATE: ".$error['SQLSTATE']."<br/>";
        echo "Code: ".$error['code']."<br/>";
        echo "Message: ".$error['message']."<br/>";
    }
}
?>
```
浏览器指向http://localhost/testsql.php(http://localhost:8080/testsql.php在 macOS 上)。 你现在应能够连接到你的 SQL Server/Azure SQL 数据库。

## <a name="see-also"></a>另请参阅  
[开始使用 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[加载 Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[系统要求 Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
