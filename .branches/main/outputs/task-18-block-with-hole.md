# FreeCAD建模任务：带中心通孔的圆角长方体

做个带孔的圆角长方体。跑完脚本存盘就行，别自己验收、别核对尺寸、别出验收报告。

## 环境

FreeCAD 1.1.3 在 E:\freecad\bin，freecadcmd.exe 和 freecad.exe 同目录；宏目录配成 E:\jiaobenmulu，脚本丢这；模型存桌面 freecad 文件夹。

## 跑法

脚本先拿 freecadcmd 无头调通，GUI 只跑最终那一遍。GUI 里 Ctrl+N 新建文档，走"宏 (M)→宏…→选中脚本→执行"，别往 Python 控制台粘贴。脚本自己建文档、存盘，末尾 Body.ViewObject 设可见再 FitAll 一下，执行完成后脚本自行删除。同名 FCStd 直接盖。

开跑前把残留的 FreeCAD 进程全杀了。E:\jiaobenmulu 写不进就查一次，还不行暂存桌面 freecad 文件夹写个说明。

## 参数

草图搁 XY 平面，+Z 拉，底面 Z=0。

- 长方体：长 65 mm（X）、宽 40 mm（Y）、高 30 mm（Z），中心对原点
- 中心通孔：直径 16 mm，沿 Z 方向打穿，孔轴跟长方体中心轴（过原点 Z 轴）重合
- 顶面四条棱倒圆角 R3 mm——只倒顶面跟四个侧面相交的棱，底面棱、竖棱、孔口棱不动

## 草图

约束怎么搞都行，按坐标摆好几何再 Block 锁死也可以。全约束、单闭合线框就行，不要求构造圆加等长那套。

## 建模

全用 Part Design 原生特征，塞一个 Body 里自动合成单一实体。不许用 Part 模块直接造几何体，也不许拿布尔运算拼。

## 参考

下面这些数只用来定义"做对"长啥样，建模时不用对、不用跑验收脚本、不用出结论：
- 单一 Body、单一实体
- 特征 TypeId 白名单：Sketcher::SketchObject、PartDesign::Pad、PartDesign::Pocket、PartDesign::Fillet；禁 Part 造体和布尔
- z=15 水平截面是 65×40 矩形中心带直径 16 圆孔（Part.Face(wire).Area 校验）
- 孔壁半径 8，Z∈[0,30]，贯穿
- 恰好 4 张 R3 圆角面（在顶面四条棱）
- 理论体积 ≈71562 mm³，容差 1%

## 卡点

建模脚本不能有求解器告警，有告警就换约束方案，同一个方案最多试两次。一个卡点最多想两个办法，第一个试两次没动静就换第二个，别在死路上反复横跳。脚本报错先找根因，改完整体重跑，别一行一行打补丁。

## 交付

只要 `block_with_hole_fillet.FCStd`，放桌面 freecad 文件夹。脚本、验收报告啥的都不用交。

## 验收核对清单（Checklist）

```plaintext
1. 长方体主体 65×40×30 mm，中心对原点，XY 平面草图、+Z 拉伸、底面落在 Z=0
2. block_with_hole_fillet.FCStd 存放在桌面 freecad 文件夹，打开无损坏
3. E:\jiaobenmulu 中无本次建模脚本残留
4. 中心通孔直径 16 mm，沿 Z 方向贯穿，孔轴与长方体中心轴重合
5. 全部特征归属同一 Body，模型为单一实体，TypeId 均在白名单内，无 Part 造体或布尔运算
6. 顶面四条棱均倒 R3 mm 圆角
7. 模型体积约 71562 mm³，偏差不超过 1%
```
