这是我自用的魔改版，目前主要是一些数值的调整，增加（对于我来说）的平衡性和可玩性

下载地址 [Release](https://github.com/CHanzyLazer/gregtech6-CH_Edition/releases)

[OmniOcular](https://github.com/CHanzyLazer/OmniOcular_GT6CHE)

不推荐在 1.0 版本之前正式游玩，因为后续更新可能会对前期的机器进行大改，可能会让存档的机器失效

# License

This Mod is licensed under the [GNU Lesser General Public License](LICENSE).
All assets, unless otherwise stated, are dedicated to the public domain
according to the [CC0 1.0 Universal Public Domain Dedication](src/main/resources/LICENSE.assets).
Any assets containing the [GregTech logo](src/main/resources/logos) or any
derivative of it are licensed under the
[Creative Commons Attribution-NonCommercial 4.0 International Public License](src/main/resources/LICENSE.logos).

# Changelog
## CH-0.1
- 配置文件：额外添加配置文件在 config/gregtechCH 文件夹，可以调整大部分数据
- 燃油引擎：现在可以在在配置文件选择禁用
- 燃油引擎：效率减少到 30%
- 燃油引擎：修改了合成表，现在耗材增加到了 80.5 个相应的材料
- 蒸汽锅炉：修改蒸汽锅炉的蒸馏水消耗逻辑，现在无论蒸汽锅炉 效率/钙化程度 为多少，消耗 1L 蒸馏水永远产生 160L 蒸汽
- 蒸汽锅炉：修改蒸汽锅炉超频逻辑，现在蒸汽锅炉可以连续超频了，也就是，在气压从 1/2 增加到 3/4 时，释放的蒸汽速率在 1 倍到 2 倍之间连续增加（超过 3/4 时固定为 2 倍）
- 蒸汽锅炉：为蒸汽锅炉额外添加了一个全局效率，现在蒸汽锅炉的实际效率为 `钙化程度效率 * 全局效率`
- 蒸汽锅炉：普通蒸汽锅炉全局效率为 50%，致密蒸汽锅炉全局效率为 60%
- 蒸汽涡轮：修改了蒸汽涡轮转换能量的逻辑，现在输出应该更加稳定了
- 燃烧室：  除了砖头燃烧室和流化床燃烧室，其余所有燃烧室的产热翻倍
- 核反应堆：工业冷却剂下燃料棒向周围释放中子数的 4 倍消弱到原来的 3/8，即 1.5 倍

## CH-0.2 (WIP)
- 配置文件：现在主要配置文件改为用 json 存储，并且实现了配置文件修改合成表，例如对于铅固体燃烧室，对应合成表的属性为：
`"recipeObject":["PCP","PwP","BBB","B","Blocks:brick_block","P","OreDictItemData:plateLead","C","OreDictItemData:plateDoubleAnyCopper"]`，
大写字母`"P", "C", "B"`代指物品（没有实际意义），在后面统一定义，物品格式为 `[格式名]:[物品名]`，支持的格式名有：
- `OreDictItemData`，GT6 添加的矿物词典，可以识别对应材料
- `OD`，GT6 类 `gregapi.data.OD` 中添加的矿物词典
- `Blocks`，Minecraft 类 `net.minecraft.init.Blocks` 中添加的原版方块
- `Items`，Minecraft 类 `net.minecraft.init.Items` 中添加的原版物品
- `ore`，矿物词典，注意这个不能识别出材料
- `[任意已加载的 ModID]`，可以添加其他 mod 的物品

# 加入项目
如果你也有魔改 GT6 的想法，欢迎加入这个项目，目前我发现的指令：
- `./gradlew setupDevWorkspace setupDecompWorkspace` 设置工作环境
- `./gradlew assemble` 打包到 `build\lib`
- `./gradlew clean` 清理工作区
- `./gradlew runClient` 在客户端上运行
- `./gradlew runServer` 在服务端上运行
- 可以组合使用，例如 `./gradlew clean setupDevWorkspace setupDecompWorkspace`，清理并重新设置工作环境

# TODO
## 数值调整
### 蒸汽相关
- 为所有材料种类设置一个基准效率，而对应机器效率和基准效率有关
- 蒸汽涡轮效率 40%
- 蒸汽引擎效率 33%
- 大型锅炉效率 80%，大型蒸汽涡轮效率效率 70%
- 蒸馏水输出效率调整，小型90%，大型98%
- 大型燃气涡轮效率 60%
- 燃气涡轮核心需要钻石晶体处理器
- 修正一下一套蒸汽发电刚好卡在过载边缘的问题（也可能是 greg 故意为之？），现在一套下来应该要刚好超过电压线，具体数值待定

### 电力相关
- 小发电机效率 60%
- 大发电机效率 95%
- 红石通量发电机效率 10%，并且增加关闭这个机器的配置，主要由于 rf 的变态机器太多
- 调低锂电池容量

### 核裂变相关
- 增殖棒需要中子数提升5-10倍

## 机制微调
### 能源相关
- 燃油引擎燃气涡轮需要点火
- 大型燃气轮机需要点火
- 增加更多种类的热交换器和大型热交换器（产热待定）

### 生产相关
- 离心废水不再能直接得到金属粉而是离心矿物
- 离心岩浆不再能直接得到金属粒而是离心矿物
- 焦炉处理离心煤现在会得到 5 个焦煤小块和 1 个焦煤小粒（而不是原本的 6 个焦煤小块）

## 机制调整
### 能源相关
- 大型蒸汽涡轮和大型燃气轮机可以调整长度，越长效率越高（存在极限并且不是线性的）
- 大型发电机中心轴改为大型磁化杆部件

### 生产相关
- 油泉会产量逐渐下降
- 压模器考虑还需要输入ku
- 搅拌机（或类似机器）的流体槽流体可以改变排序，并且可以切换模式直接从输出口输出（可以通过红石和覆盖版实现自动化）
- 更多种类的大型机器
- 添加检测锅炉材料的传感器

### 铬相关（待定）
- 添加铬铁合金，可用于制造不锈钢（同理镍铬合金也能做不锈钢）
- 铬铁矿不再能直接从坩埚炼出铬，而是使用碳还原出铬铁合金，1523k
- 铬铁合金离心耗能增加
- 铬的合成路线修改，可能会参考 gt6u （待定）

### 其他金属生产路线改动（待定）

### 化工线的补充完善（待定）

### 核裂变相关
- 枯竭棒可离心出其他产物，如铀的可出铅
- 将原本的线性路线升级燃料棒改成网状路线升级
- 添加新的燃料棒（待定）

## 机制大改
### 能源相关
- 涡轮，燃油引擎（可能是引擎核心？），大型的涡轮，改为外置转子，输出由转子和外壳共同决定
- 增加转子磨损，并且可以有方法自动化替换转子，坏的转子可以回收大部分材料

### 生产相关
- 坩埚机制大改，在发生反应时会停止升温并根据反应类型来逐渐转换
- 多个输入能量的机器
- 让齿轮箱和轴等 RU 设备有用起来
- 修改粉末的机制，让粉末的管理和处理都更加简单直接，不让再一大堆 1/72 粉填满背包
- 目前思路有：存储粉末的储物桶能直接调整粉末类型（对应输出类型不改变容量）；
- 搅拌器等需要粉末合成的机器，增加和流体类似的粉末槽，使用和储物桶类似的方法存储和反应；
- 粉末槽和流体一样，可以通过外接漏斗和“水龙头”来交互输出，不过粉末槽也可以从一般的物品槽输入粉末；
- 燃烧室的灰烬也采用类似的逻辑
