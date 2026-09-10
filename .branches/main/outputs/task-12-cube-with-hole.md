# FreeCAD建模任务：带中心通孔的倒角正方体

做一个正方体，中心打个通孔，顶面四条棱倒个角。只建模存盘，不要自行验收、不要核对尺寸、不要生成验收报告，存完即完成。

## 环境信息

FreeCAD 1.1.3 在 E:\freecad\bin（freecadcmd.exe 和 freecad.exe 同目录）；宏目录配成 E:\jiaobenmulu，脚本放这；模型存桌面 freecad 文件夹。

## 怎么跑

脚本和 freecadcmd 无头调试先搞，不用等 GUI。GUI 里 Ctrl+N 新建文档，再"宏 (M)→宏…→选中脚本→执行"跑一次。别用 Python 控制台粘贴。

脚本自己建文档、存盘，末尾 Body.ViewObject 设可见 + FitAll 一次。同名 FCStd 直接覆盖。

启动前先清残留 FreeCAD 进程。E:\jiaobenmulu 写不进就排查一次，还不行暂存桌面 freecad 文件夹注明。

## 尺寸

草图 XY 平面，+Z 拉伸，底面 Z=0。

- 正方体：边长 50 mm（X、Y、Z 方向均 50 mm），中心对原点
- 中心通孔：直径 20 mm，沿 Z 方向贯穿，孔轴与正方体中心轴（过原点 Z 轴）重合
- 顶面四条棱倒角 C3 mm——仅顶面与四个侧面相交的棱，底面棱、竖棱、孔口棱不倒

## 草图

约束方式不限，按坐标摆几何再 Block 锁位也行。要求全约束、单闭合线框。不强制构造圆加等长。

## 规矩

全用 Part Design 原生特征，同一个 Body，自动合成单一实体。禁 Part 模块直生几何体，禁布尔拼接。

## 理论值（仅定义正确性，不需要执行验收）

以下数值用于定义"做对"的标准，建模时不需要核对、不需要跑验收脚本、不需要输出验收结论：
- 单一 Body、单一实体
- 特征 TypeId 白名单：Sketcher::SketchObject、PartDesign::Pad、PartDesign::Pocket、PartDesign::Chamfer；禁 Part 造体和布尔
- z=25 水平截面为 50×50 正方形中心带直径 20 圆孔（Part.Face(wire).Area 校验）
- 孔壁半径 10，Z∈[0,50]，贯穿
- 恰好 4 张 C3 倒角面（位于顶面四条棱）
- 理论体积 ≈108392 mm³，容差 1%

## 调试和卡点

建模脚本零求解器告警，告警即换约束方案，同一方案最多试两次。

一个卡点最多想两个办法，第一个试两次没进展就换第二个，别重复失败路径。脚本报错先查根因，改完整体重跑，不逐行打补丁。

## 交什么

只要 `cube_with_hole_chamfer.FCStd`，存桌面 freecad 文件夹。脚本、验收报告之类不用交。

## 验收核对清单（Checklist）

```plaintext
1. cube_with_hole_chamfer.FCStd 位于桌面 freecad 文件夹，文件可正常打开无损坏
2. 模型为单一 Body 下的单一实体，特征 TypeId 均在白名单内，无 Part 造体或布尔运算
3. 正方体边长 50 mm，中心对原点，XY 草图、+Z 拉伸、底面 Z=0
4. 中心通孔直径 20 mm，沿 Z 方向贯穿，孔轴与正方体中心轴重合
5. 顶面四条棱倒角 C3 mm，其余棱未倒角
6. 模型体积 ≈108392 mm³，偏差在 1% 以内
```
