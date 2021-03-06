# 第1章、Sql server数据库基本概念

## 1.1、逻辑数据库

### 1.1.1、数据库对象

数据库对象包括：表（table）、试图（View）、索引（index）、存储过程（Store Procedure）、触发器（trigger）等

| 对象     | 对象的描述                                                   |
| -------- | ------------------------------------------------------------ |
| 表       | 包含数据库中所有数据的数据库对象，由行和列构成，是最重要的数据库对象 |
| 视图     | 由一个表或多个表导出的表，又称为虚拟表（支持操作的同时更新） |
| 索引     | 加快数据检索速度并可以保证数据唯一性的数据结构               |
| 存储过程 | 为完成特定功能的T-SQL语句集合，编译后存放在服务器端的数据库中 |
| 触发器   | 一种特殊的存储过程，当某个规定的事件发生时，该存储过程自动执行 |

### 1.1.2、系统数据库和用户数据库

1、系统数据库

软件安装默认创建4个数据库，目的是存储有关SQL Server的系统信息，当系统数据库收到破坏时，SQL server将不能正常启动和工作

| 数据库 | 功能                                                         |
| ------ | ------------------------------------------------------------ |
| master | 系统最重要的数据库，记录SQL server的系统信息，用来控制用户数据库和SQL Server的运行。如账号登录、系统配置、数据库位置、数据库错误信息等 |
| model  | 为创建数据库提供模板                                         |
| msdb   | 该数据库是代理服务数据库，为调度信息、作业记录等提供存储空间 |
| tempdb | 临时数据库，为临时表和临时存储过程提供存储空间               |

2、用户数据库

用户数据库就是由用户创建的数据库。用户数据库和系统数据库在结构上是相同的

### 1.1.3、完全限定名和部分限定名

1、完全限定名

即对象的全名（SQL Server创建的每个对象都有唯一的完全限定名），由服务器名、数据库名、数据库架构名、对象名4部分组成。

完全限定名的格式：Server.database.schema.object， 例如：DELL_PC.stsc.dbo.student就是一个完全限定名

2、部分限定名

使用完全限定名通常较为繁琐且没有必要，所以通常会省略其中的某些部分。前3部分均可被省略。若省略中间部分时，圆点符.不能省略，即（在部分限定名中，未指出的部分使用以下默认值）

| 部分限定名称 | 默认值           |
| ------------ | ---------------- |
| 服务器       | 默认为本地服务器 |
| 数据库       | 默认为当前数据库 |
| 数据库架构名 | 默认为dbo        |

## 1.2、物理数据库

### 1.2.1、页和区

页和区是SQL server数据库的两个主要数据存储单位

| 页   | 每个页的大小是8KB，每1MB的数据文件可以容纳128页，页是SQL server中数据存储的最基本单位 |
| ---- | ------------------------------------------------------------ |
| 区   | 每8个连接的页组成一个区，区的大小是64KB，1MB的数据库有16个区，区用来控制表和索引的存储 |

### 1.2.2、数据库文件

qlserver采用操作系统文件来存放数据库，使用的文件有主数据文件、辅助数据文件、日志文件3类

| 文件种类                    | 文件类型功能描述                                             |
| --------------------------- | ------------------------------------------------------------ |
| 主数据文件（primary）       | 用来存储数据，每个数据库必须有且只能有一个主文件，默认后缀.mdf |
| 辅助数据文件（secondary）   | 也用来存储数据，一个数据库中辅助文件可以创建多个，也可以没有，默认后缀.ndf |
| 日志文件（transaction Log） | 用来保存恢复数据库所需的事务日志信息，每个数据库至少有1个日志文件，默认后缀.ldf |

### 1.2.3、数据库文件组

在数据库中，为管理和分配数据将多个文件组织在一起，组成文件组。对文件进行整体管理，以提高表中数据的查询效率。

SQL Server提供了两类文件组：主文件组和用户定义文件组

| 文件组分类     | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| 主文件组       | 包含主要数据文件和任何没有指派给其他文件组的文件，数据库的系统表均分配到主文件组中 |
| 用户定义文件组 | 包含使用"create database"或“alter database”语句并使用“filegroup”关键字指定的文件组 |

# 第2章、SQL Server数据类型

## 2.1、数据类型总结表

| 数据类型      | 标识符                                                       |
| ------------- | ------------------------------------------------------------ |
| 整数型        | bigint、int、smallint、tinyint                               |
| 精确数值型    | decimal、numeric                                             |
| 浮点型        | float、real                                                  |
| 货币型        | money、smallmoney                                            |
| 位型          | bit                                                          |
| 字符型        | char、varchar、varchar(MAX)                                  |
| Unicode字符型 | nchar、nvarchar、nvarchar(MAX)                               |
| 文本型        | text、ntext                                                  |
| 二进制型      | binary、varbinary、varbinary(MAX)                            |
| 日期时间类型  | datetime、smalldatetime、date、time、datetime2、datetimeoffset |
| 时间戳型      | timestamp                                                    |
| 图像型        | image                                                        |
| 其他          | cursor、sql_variant、table、uniqueidentifier、xml、hierarchyid |

## 2.2、各类数据类型详述

### 2.2.1、整数型

| 类型标识符          | 范围描述                                         |
| ------------------- | ------------------------------------------------ |
| bigint（大整数）    | 精度19位，长度8字节，数值范围：-2 ^63 ~ 2^63 - 1 |
| int（整数）         | 精度10位，长度4字节，数值范围：-2 ^31~ 2^31 - 1  |
| smallint（短整数）  | 精度10位，长度2字节，数值范围：-2 ^15~ 2^15 - 1  |
| tinyint（微短整数） | 精度3位，长度1字节，数值范围：0~255              |

### 2.2.2、精确数值型

精确数值性由整数部分和小数部分构成，可存储10^38+1到10^38-1的固定精度和小数位的数字数据，存储长度为5~17个字节

数据格式是：numeric | decimal（p [,s]），其中p为精度，s为小数位数，s缺省值为0，举例如下：

指定某列为为精确数值型，精度为7，小数位数为2，则为decimal（7，2）

### 2.2.3、浮点型

浮点型又称近似数值型，包括float[(n)]和real两类，通常都使用科学记数法表示数据，如：4.804E9，3.682-E6，78594E-8等

| 类型标识符 | 范围描述                                                     |
| ---------- | ------------------------------------------------------------ |
| real       | 精度为7为，长度为4字节，数值范围：-3.40E + 38~3.40E+38       |
| float[(n)] | 当n在1~24之间时，精度为7位，长度位4字节，数值范围：-3.40E + 38~3.40E+38 |
|            | 当n在25~53之间时，精度位15位，长度为8字节，数值范围：-1.79E308~1.79E+308 |

### 2.2.4、货币型

处理货币的数据类型有money和smallmoney，他们用十进制数表示货币值

| 类型标识符 | 范围描述                                                     |
| ---------- | ------------------------------------------------------------ |
| money      | 精度为19位，小数位数为4、长度为8字节，数值范围：-2 ^63~ 2^63 - 1 |
| smallmoney | 精度为10位，小数位数为4、长度为4字节，数值范围：-2 ^31~ 2^31 - 1 |

### 2.2.5、位型

只存储0和1，长度为1个字节。当一个表中有小于8位的bit列，将作为一个字节存储，若表中有9到16位bit列，将作为两个字节存储，以此类推。

### 2.2.6、字符型

字符型常用于存储字符串，在输入字符串时，需将串中的符号用单引号或双引号括起，如’def’，”def<Ghi”

| 类型标识符   | 范围描述                                                     |
| ------------ | ------------------------------------------------------------ |
| char[(n)]    | 固定长度字符数据类型，其中n定义字符型数据的长度，n在1~8000之间，默认值为1.若输入字符串长度小于n时，系统自动在其后添加空格以达到长度n，例如：某列的数据类型是char(100)，若输入的字符串是“NewYear2013”，则存储的是字符New Year2013和89个空格。若输入的字符串长度大于n，则自动截断超出的部分 |
| varchar[(n)] | 可变长度字符数据类型，其中n的规定与定长字符数据类型char[(n)]中的n完全相同，与char[(n)]不同的是varchar[(n)]数据类型的存储空间随列值的字符数而变化。例如：表中某列的数据类型为varchar[(n)]，输入的字符串为“NewYear2013”，则存储的字符是NewYear2013长度11个字节，其后不添加空格 |

### 2.2.7、Unicode字符型

Unicode是“统一字符编码标准”，用来支持国际上非英语语种的字符数据的存储和处理

| 类型标识符    | 范围描述                                                     |
| ------------- | ------------------------------------------------------------ |
| nchar[(n)]    | 固定长度Unicode数据的数据类型，n的取值1~4000，长度为2n字节，若输入的字符串长度不足n，将以空白符补足 |
| nvarchar[(n)] | 可变长度Unicode数据的数据类型，n的取值为1~4000，长度是所输入的字符个数的两倍 |

### 2.2.8、文本型

由于字符型数据的最大长度为8000个字符，当存储超出则不能满足应用需求（如：较长的备注/日志等），文本型包括text和ntext两类，分别对应ASCII字符和Unicode字符

| 类型标识符 | 范围描述                                                     |
| ---------- | ------------------------------------------------------------ |
| text       | 最大长度为2^31-1个字符（2，147，483，647），存储字节数与实际字符个数相同 |
| ntext      | 最大长度2^30-1个Unicode字符（1，073，741，823），存储字节数是实际字符个数的2倍 |

### 2.2.9、二进制型

二进制数据类型表示的是位数据流，包括binary（固定长度）和varbinary（可变长度）两种

| 类型标识符     | 范围描述                                                     |
| -------------- | ------------------------------------------------------------ |
| binary[(n)]    | 固定长度的n个字节二进制数据，n取值1~8000，默认为1。binary（n）数据的存储长度为：n+4个字节。若输入的数据长度小于n，则不足部分用0填充，若输入数据长度大于n，则多余部分被截取。输入二进制时，在数据前要是加上0x，可以用的数字符号位0~9/A~F（字符大小写均可）。由于每个字节的最大数为FF，所以在0x格式的数据每两位占1个字节，二进制数据有时也被称为十六进制数据 |
| varbinary[(n)] | n个字节变长二进制数据，n取值1~8000，默认值为1，存储长度为实际输入数据长度+4个字节 |

### 2.2.10、日期时间类型

| 类型标识符     | 范围描述                                                     |
| -------------- | ------------------------------------------------------------ |
| datetime       | 可表示的日期范围从1753年1月1日到9999年12月31日的日期和时间数据，精确度为百分之三秒（3.33毫秒或0.00333秒）。datetime类型数据长度为8字节，日期和时间分别使用4个字节存储，正数表示日期为1900年1月1日之后，负数则表示日期在1900年1月1日之前。后4个字节用于存储距12：00（24小时制）的毫秒数。默认的日期时间是：January 1，1900 12：00 A.M 。可以接受的输入格式有：January 10 2012、Jan 10 2012、JAN 10 2012、January 10，2012等 |
| smalldatetime  | 与datetime类似，但日期时间范围较小，表示从1900年1月1日到2079年6月6日的日期和时间，存储长度为4个字节 |
| date           | 可表示从公元元年1月1日到9999年12月31日期，表示形式与datetime数据类型的日期部分相同，只存储日期数据，不存储时间数据，存储长度为3个字节 |
| time           | 只存储时间数据，格式为“hh:mm:ss[.nnnnnnn]”,hh表示小时，范围1~23，mm表示分钟，范围0~59，ss表示秒数，范围0~59。n是0到7位数字，范围从0到9999999，表示秒的小数部分，即微秒数。所以time数据类型的取值范围为00：00：00.0000000到23：59：59.9999999。time类型的存储大小为5个字节。另外可以自定义time类型微秒数的位数，例如：time（1）表示小数位为1，默认为7 |
| datetime2      | 新的datetime2数据类型和datetime类型一样，也是存储日期和时间信息。但是datetime2类型取值范围更广，日期部分取值范围从公元元年1月1日到9999年12月31日，时间部分的取值范围是00：00：00.0000000到23：59：59.9999999，另外，用户还可以自定义datetime2数据类型中微秒数的位数，例如：datetime2（2）表示小数位数为2 |
| datetimeoffset | 也是用于存储日期和时间信息，取值范围与datetime2类型相同，但datetimeoffset类型具有时区偏移量，此偏移量指定时间相对于协调世界时（UTC）偏移的小时和分钟数。datetimeoffset的格式为YYYY-MM-DD hh:mm:ss[.nnnnnnn] [{+\|-}hh:mm]，其中hh为时区偏移量中的小时数，范围从00到14，mm为时区偏移量中的额外分钟数，范围从00到59 |

### 2.2.11、时间戳型

反应系统对该记录修改的相对顺序（相对与其他记录），表示符是timestamp，timestamp类型数据的值是二进制格式数据，其长度为8字节。若创建表时定义一个列的数据类型为时间戳类型，那么每当对该表加入新行或修改已有行时，都由系统自动讲一个计数器值加到该列，即将原来的时间戳值加上一个增量

### 2.2.12、图像数据类型

用于存储图片、照片等，标识符为image，实际存储的时可变长度二进制数据，介于0~231-1个字符（2，147，483，647）

### 2.2.13、其他数据类型

| 类型标识符       | 范围描述                                                     |
| ---------------- | ------------------------------------------------------------ |
| cursor           | 游标数据类型，用于创建游标变量或定义存储过程的输出参数       |
| sql_variant      | 一种存储SQL Server支持的各种数据类型（除text/ntext/image/timestamp/sql_variant之外）值的数据类型 |
| table            | 用于存储结果集的数据类型，结果集可以供后续处理               |
| uniqueidentifier | 唯一标识符类型，系统将为这种类型的数据产生唯一标识值         |
| xml              | 用来在数据库中保存xml文档和片段的一种类型，文件大小不能超过2GB |
| hierarchyid      | Sql server2008新增加的一种长度可变的系统数据类型，可使用hierarchyid表示层次结构中置 |

