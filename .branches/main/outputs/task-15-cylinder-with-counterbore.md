# FreeCAD建模任务：带沉孔的圆角圆柱

本次建模目标：一个带沉孔的圆柱。建模完成后直接保存文件即可，不需要自行验收、不需要核对尺寸、不需要生成验收报告。

## 建模参数

草图放在 XY 平面，沿 +Z 方向拉伸，底面落在 Z=0。

- 主体圆柱：直径 60 mm，高 25 mm，圆心对原点
- 顶面中心沉孔：沉头直径 22 mm、深 5 mm（自顶面名义面向下量），下方通孔直径 10 mm 贯穿至底面，孔轴与圆柱中心轴（过原点 Z 轴）重合
- 顶面外圆倒圆角 R2 mm——仅顶面与侧面相交的外圆环棱，底面棱、孔口棱不倒

## 环境和执行

FreeCAD 1.1.3 装在 E:\freecad\bin，freecadcmd.exe 和 freecad.exe 同目录；用户宏目录已配为 E:\jiaobenmulu，脚本存该目录；模型存桌面 freecad 文件夹。

脚本可以先用 freecadcmd 无头调试，不必等 GUI。GUI 里 Ctrl+N 新建文档后走"宏 (M)→宏…→选中脚本→执行"跑一次，别走 Python 控制台粘贴。脚本负责自建文档、存盘，末尾 Body.ViewObject 设可见再 FitAll 一次。同名 FCStd 直接覆盖。

启动前先把残留 FreeCAD 进程全结束掉。E:\jiaobenmulu 写不进去就排查一次，还不行暂存桌面 freecad 文件夹并注明。

## 草图和建模

草图约束方式不限，按坐标摆几何再 Block 锁位也行，要求全约束、单闭合线框，不强制构造圆加等长。

全部用 Part Design 原生特征，塞进同一个 Body 自动合成单一实体。禁 Part 模块直生几何体，禁布尔拼接。

## 参考值

以下数值仅用于定义"做对"的标准，建模时不需要核对、不需要跑验收脚本、不需要输出验收结论：
- 单一 Body、单一实体
- 特征 TypeId 白名单：Sketcher::SketchObject、PartDesign::Pad、PartDesign::Pocket、PartDesign::Fillet；禁 Part 造体和布尔
- z=12.5 水平截面为直径 60 的圆（Part.Face(wire).Area 校验）
- 沉孔沉头半径 11，Z∈[20,25]；通孔半径 5，Z∈[0,25]
- 恰好 1 张 R2 圆角面（位于顶面外圆棱）
- 理论体积 ≈67056 mm³，容差 1%

## 注意事项

建模脚本零求解器告警，告警即换约束方案，同一方案最多试两次。一个卡点最多想两个办法，第一个试两次没进展就换第二个，别重复失败路径。脚本报错先查根因，改完整体重跑，不逐行打补丁。

## 交付

只要 `cylinder_with_counterbore_fillet.FCStd`，存桌面 freecad 文件夹。脚本和验收报告不用交。

## 验收核对清单（Checklist）

```plaintext
1. 主体圆柱直径 60 mm、高 25 mm，圆心对原点，XY 平面草图、+Z 拉伸、底面落在 Z=0
2. 顶面中心沉孔沉头直径 22 mm、深 5 mm，下方通孔直径 10 mm 贯穿，孔轴与圆柱中心轴重合
3. 顶面外圆环棱倒 R2 mm 圆角
4. 全部特征归属同一 Body，模型为单一实体，TypeId 均在白名单内，无 Part 造体或布尔运算
5. cylinder_with_counterbore_fillet.FCStd 存放在桌面 freecad 文件夹，打开无损坏
6. 模型体积约 67056 mm³，偏差不超过 1%
```
