# GIS-RS-Learning
记录一些GIS和RS的东西

## Markdown 语法

- 链接代码

如果代码文件和README.md文件在同一目录下，你只需要文件名。

在README.md文件中，使用Markdown的链接语法创建链接。链接的语法是[链接文本](链接地址)，其中“链接文本”是你希望在README.md中显示的文本，而“链接地址”是代码文件的相对路径。

[示例代码](src/example.py)

可以直接copy path

- 插入图片
```
![替代文本](images/image.png)
![替代文本](https://example.com/path/to/image.png)
![替代文本](https://raw.githubusercontent.com/username/repository/branch/path/to/image.png)
# 调整图片尺寸 虽然GitHub的Markdown解析器不支持Markdown语法中的图片尺寸调整，但它允许你在Markdown文件中使用一些HTML标签。
<img src="image.png" width="100" height="100">


```
- 表情 :smile:
在GitHub的README.md文件中插入表情符号可以通过使用GitHub支持的表情符号简码（Emoji shortcode）来实现。这些简码以冒号:开始和结束，中间是表情符号的名称。例如，:smile:将显示为一个笑脸表情符号 😄。
# 并行和多线程
要获取当前CPU的核心数和系统的内存信息，你可以使用Python的psutil库。psutil（process and system utilities）是一个跨平台库，用于访问系统详细信息和资源使用情况，如CPU、内存、磁盘、网络等。
- 物理核心数（Physical Cores）：
  - 物理核心指的是CPU中实际存在的处理核心数量。每个物理核心都是一个独立的处理单元，拥有自己的运算和执行资源，如算术逻辑单元（ALU）和寄存器。
  - 物理核心数是CPU能够同时处理任务或线程的物理限制。一个物理核心在同一时间内通常只能执行一个任务或线程。
- 逻辑核心数（Logical Cores）：
  - 逻辑核心数通常与超线程技术有关。超线程是一种使单个物理CPU核心能够像两个逻辑处理单元一样工作的技术，从而提高处理效率和并发能力。
当超线程被启用时，操作系统和应用程序会将每个物理核心视为两个“逻辑”核心。因此，逻辑核心数可能是物理核心数的两倍（假设每个物理核心支持两个线程）。
  - 逻辑核心通过在物理核心的不同执行阶段交错执行两个线程，从而尝试利用执行单元的空闲周期，提高CPU的整体效率。
- 举例说明：
假设一个CPU有4个物理核心，并且支持超线程技术。那么，这个CPU将有4个物理核心和8个逻辑核心。操作系统和应用程序会看到8个可用的处理单元（核心），尽管实际上只有4个是物理存在的。
```python
import psutil

# 获取物理核心数（不考虑超线程）
physical_cores = psutil.cpu_count(logical=False)
print(f"Physical CPU cores: {physical_cores}")

# 获取逻辑核心数（考虑超线程）
logical_cores = psutil.cpu_count(logical=True)
print(f"Logical CPU cores: {logical_cores}")

# 获取内存信息
memory_info = psutil.virtual_memory()

# 总内存
total_memory = memory_info.total / (1024 ** 3)  # 转换为GB
print(f"Total memory: {total_memory:.2f} GB")

# 可用内存
available_memory = memory_info.available / (1024 ** 3)  # 转换为GB
print(f"Available memory: {available_memory:.2f} GB")


```
Physical CPU cores: 128
Logical CPU cores: 128
Total memory: 251.60 GB
Available memory: 215.11 GB
## gkpg文件和shapefile文件的差别是什么?
GeoPackage (GPKG) 文件和 Shapefile 是两种常用的地理空间数据格式，它们在地理信息系统（GIS）中用于存储、交换和管理地理空间数据。这两种格式在结构和功能上有一些关键的差异：

**GeoPackage (.gpkg)**

标准：GeoPackage 是一种基于 SQLite 的开放标准，由开放地理空间联盟（OGC）维护。

文件结构：GeoPackage 是一个容器，可以在单个 .gpkg 文件中存储多种类型的地理空间数据和瓦片地图数据。

数据类型：支持矢量数据（如点、线、面）和栅格数据（如地图瓦片）的存储。

扩展性和灵活性：由于基于 SQLite，GeoPackage 支持高级数据库功能，如索引、SQL查询和触发器，使其更加灵活和可扩展。

互操作性：良好的跨平台支持和与现代GIS软件的兼容性，如 QGIS 和 ArcGIS。

**Shapefile (.shp, .shx, .dbf, 等)**

标准：Shapefile 是由 ESRI 开发的一种开放的，但专有的数据格式，广泛用于 GIS 软件中。

文件结构：Shapefile 实际上是由多个文件组成的一个集合，至少包括 .shp（形状数据）、.shx（形状索引）和 .dbf（属性数据）三个文件。

数据类型：主要用于存储矢量数据，如点、线和多边形。不直接支持栅格数据。

扩展性和灵活性：相对于 GeoPackage，Shapefile 在数据库功能和存储容量方面有更多的限制，例如每个字段的字符数限制和单个文件大小限制。

互操作性：由于其长期存在和广泛使用，Shapefile 有非常好的软件支持，几乎所有的 GIS 软件都能读写 Shapefile 格式。

总结
GeoPackage 是一个较新的标准，提供了更多的功能和灵活性，支持多种类型的地理空间数据在一个文件中存储，适合于需要高级数据库功能和大数据集的应用场景。
Shapefile 由于其简单和广泛的软件支持，仍然是地理空间数据交换的流行选择，尤其是在简单的地理数据集合中。
