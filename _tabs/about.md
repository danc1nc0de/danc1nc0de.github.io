---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
title: 关于博主
---

![挚爱](assets/img/with-yanyan.jpg)

<br>
<br>
> 纸上得来终觉浅，绝知此事要躬行
{: .prompt-tip }

<center>
    <h1>孙颖豪&nbsp;&nbsp;&nbsp;&nbsp;Yinghao Sun</h1>
    <div>
        <span>
            <img alt="phone" src="assets/icon/phone-solid.svg" width="18px">
            一山一柳腰凌玲无酒凄凌
        </span>
        &nbsp;&nbsp;&nbsp;&nbsp;
        <span>
            <img alt="e-mail" src="assets/icon/envelope-solid.svg" width="18px">
            bit_syh@163.com
        </span>
        &nbsp;&nbsp;&nbsp;&nbsp;
        <span>
            <img alt="github" src="assets/icon/github-brands.svg" width="18px">
            <a href="https://github.com/danc1nc0de">Github</a>
        </span>
        &nbsp;&nbsp;&nbsp;&nbsp;
        <span>
            <img alt="blog" src="assets/icon/rss-solid.svg" width="18px">
            <a href="https://yinghao.info">Blog</a>
        </span>
    </div>
</center>

## <img alt="info" src="assets/icon/info-circle-solid.svg" width="30px"> 个人信息 

- 性&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;别：男
- 出生年月：1993年10月
- 籍&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;贯：河北保定
- 学&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;历：博士
- 研究方向：机器人感知算法、多传感器融合、多目标跟踪、信号处理相关
- 爱&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;好：游泳、端游、Coding

## <img alt="graduation" src="assets/icon/graduation-cap-solid.svg" width="30px"> 教育经历

- 博士学位，北京理工大学，信息与通信工程专业，2016年9月～2022年7月
  - 雷达技术研究所，导师毛二可院士
  - 以第 1 作者已发表 SCI 论文 5 篇（含顶刊 4 篇），EI 论文 3 篇，中文核心 2 篇；已授权发明专利 6 项
- 学士学位，北京理工大学，电子科学与技术专业，2012年9月～2016年7月
  - 本科期间专业排名 2 / 60+，保送研究生
- 高中，河北保定第一中学，理科，2009年9月～2012年7月
  - 高考成绩 659 分，全校排名 8 / 900+，河北省排名 748 / 22w+，考取北京理工大学

## <img alt="work" src="assets/icon/briefcase-solid.svg" width="30px"> 工作经历

- **2022年7月～至今，深圳大疆创新科技有限公司，车载动态感知部门，高级计算机视觉算法工程师**

    > 2023年大疆车载已独立经营，成立深圳市卓驭科技有限公司
    {: .prompt-info }

    工作期间主要负责辅助驾驶系统中的**多传感器后融合**、**多目标跟踪**、**场景融合（智能大灯相关）**相关算法的开发迭代及部署落地。

    从**0**开始，**独立完成算法预研、架构设计、算法开发、代码移植、部署上线、算法迭代**等，完成大疆车载**多传感器融合&多目标跟踪&场景融合**整体算法的**更新换代**，并在多家OEM发布车型中**量产**，融合跟踪效果相比上一代算法在目标车**大幅转向/掉头、倒车、缓慢加塞、遮挡**等多种场景有**显著提升**。

    工作期间了解熟悉机器人领域智能感知相关算法，包括但不限于 Stereo, 2D Detection, Mono 3D Detection, Scene Flow, Bev 3D Detection, Occupancy, Radar Detection, Optical Flow, Time to Collosion Estimation, Trajectory Prediction 等。

## <img alt="research" src="assets/icon/project-diagram-solid.svg" width="30px"> 科研经历

- **面向强杂波环境的机载雷达捷变波形设计与信号处理技术研究**

    围绕强杂波环境下机载雷达中的捷变波形设计和信号处理技术，分别从捷变波形发射序列设计与优化、捷变波形失配滤波处理以及折叠杂波分离与抑制三个方面展开研究，项目创新点和主要成果如下：

  1. 针对机载雷达中捷变波形发射序列设计与优化问题，本文从捷变波形自身及其发射序列优化两个角度，分别基于脉间初相捷变和脉间调频捷变两类捷变波形提出相关优化算法，充分利用雷达发射端自由度解决目标距离模糊问题，实现对折叠杂波的初步抑制，仿真结果验证了所提算法的有效性。
  2. 针对波形捷变带来的距离旁瓣调制效应，本文提出一种基于动态交替投影的失配滤波器设计算法，并给出可避免矩阵求逆的快速算法，可以在低计算复杂度、信号处理损失可控的条件下优化设计失配滤波器，实现在多种优化指标下对多种捷变波形的失配滤波输出旁瓣抑制或旁瓣对齐，有效改善距离旁瓣调制效应，仿真结果验证了所提算法的有效性。
  3. 针对捷变波形发射序列在距离-多普勒成像平面输出旁瓣较高的问题，本文提出一种基于距离-多普勒二维旁瓣抑制的失配滤波器设计算法，可以在信号处理损失可控的条件下优化设计失配滤波器，有效抑制距离-多普勒成像平面指定区域的二维高旁瓣，改善旁瓣遮蔽效应，仿真与实测数据处理结果验证了所提算法的有效性。
  4. 针对机载雷达中折叠杂波抑制问题，本文提出一种基于交替重构反演的折叠杂波分离与抑制算法，充分利用杂波在距离-多普勒维和空域-多普勒维分布特性实现对不同距离段杂波回波的重构反演，有效分离并抑制折叠杂波。所提算法适用于脉间初相捷变和脉间调频捷变两类捷变波形，并给出计算精度和计算复杂度可权衡的闭式解和迭代解两种算法求解方式，仿真与实测数据处理结果验证了所提算法的有效性。

  综上，本项目针对强杂波环境下机载雷达中的捷变波形设计和信号处理技术展开研究，充分利用雷达发射端和接收端自由度实现对不同距离段杂波回波的重构反演，有效分离并抑制折叠杂波，改善机载雷达中的距离模糊和杂波折叠问题，提高机载雷达在强杂波环境中的目标探测性能。

<div style="display: flex; justify-content: center; align-items: center;">

<div style="text-align: center; margin: 0 20px;">
  <img src="assets/img/folded-clutter-before.jpg" alt="Image 1" style="width: auto; height: auto; display: block; margin: 0 auto;">
  <p style="margin: 10px 0 0;">折叠杂波（重构前）</p>
</div>

<div style="text-align: center; margin: 0 20px;">
  <img src="assets/img/folded-clutter-after.jpg" alt="Image 2" style="width: auto; height: auto; display: block; margin: 0 auto;">
  <p style="margin: 10px 0 0;">折叠杂波（重构后）</p>
</div>

</div>

## <img alt="skill" src="assets/icon/tools-solid.svg" width="30px"> 技能清单

- ★★★★☆ 熟悉C++ & Python
- ★★★★☆ 熟悉信号处理领域相关理论与算法
- ★★★★☆ 熟悉贝叶斯理论、概率论、凸优化、非线性优化等基础理论
- ★★★★☆ 熟悉卡尔曼滤波KF、扩展卡尔曼滤波EKF、无迹卡尔曼滤波UKF、粒子滤波PF等基础理论与算法
- ★★★★☆ 熟悉单/多目标跟踪中常用的 NN、PDA、GSF、GNN、JPDA、MHT 等算法框架
- ★★★☆☆ 了解机器人领域智能感知相关算法

## <img alt="demo" src="assets/icon/github-brands.svg" width="30px"> Some Demos

TODO

## <img alt="publication" src="assets/icon/graduation-cap-solid.svg" width="30px"> 已发表的论文和专利

1. **Y. Sun**, H. Fan, L. Ren, E. Mao and T. Long, “Folded Clutter Suppression for Pulse-Doppler Radar Based on Pulse-Agile Waveforms,” in IEEE Transactions on Signal Processing (SCI 一区顶刊，IF:5.4), vol. 70, pp。 3774-3788, 2022.
2. **Y. Sun**, H. Fan, J. Wang, L. Ren, E. Mao and T. Long, “Optimization of Diverse PCFM Waveforms and Joint Mismatched Filters,” in IEEE Transactions on Aerospace and Electronic Systems (SCI 二区顶刊，IF:4.4), vol. 57, no. 3, pp. 1840-1854, 2021.
3. **Y. Sun**, H. Fan, E. Mao, Q. Liu and T. Long, “Range-Doppler Sidelobe Suppression for Pulse-Diverse Waveforms,” in IEEE Transactions on Aerospace and Electronic Systems (SCI 二区顶刊，IF:4.4), vol. 56, no. 4, pp. 2835-2849, 2020.
4. **Y. Sun**, Q. Liu, J. Cai and T. Long, “A Novel Weighted Mismatched Filter for Reducing Range Sidelobes,” in IEEE Transactions on Aerospace and Electronic Systems (SCI 二区顶刊，IF:4.4), vol. 55, no. 3, pp. 1450-
5. **Y. Sun**, Q. Liu, J. Cai and T. Long, “A Novel Method for Designing General Window Functions with Flexible Spectral Characteristics,” in Sensors, vol. 18, no. 9, pp. 3081, 2018.
6. **Y. Sun**, L. Ren, H. Fan and X. Yang, “Frequency Hopped Synthetic Bandwidth Waveform Design and Processing Algorithm for Self-Speed Measurement,” in Journal of Signal Processing, vol. 35, no. 6, pp. 1034-1040, 2019.
7. **Y. Sun**, H. Fan, L. Ren and E. Mao, “Fast Algorithm for Mismatched Filter Design based on Dynamic Alternating Projection,” in Journal of Signal Processing, Accepted, 2021.
8. **Y. Sun**, Q. Liu, J. Cai and T. Long, “Fast Algorithm for Designing Unimodular Sequence and Related Mismatched Filter with Flexible Correlation Properties,” in The Journal of Engineering, vol. 2019, no. 19, pp. 5487-5492, 2019.
9. **Y. Sun**, H. Fan, R. Zhuang, L. Ren, E. Mao and T. Long, “Optimization of Pulse-agile Sequence for Suppressing Range Folded Clutter Based on Diverse NLFM Waveforms,” in 2020 IEEE Radar Conference, Florence, Italy, 2020.
10. **Y. Sun**, L. Ren, K. Zhang and E. Mao, “Unimodular Phase-coded Waveforms with Low Sidelobes over Desired Range-Doppler Regions,” in 2019 IEEE International Conference on Signal, Information and Data Processing, Chongqing, China, 2019.
11. J. Xu, J. Cai, **Y. Sun**, X. Xia, A. Farina and T. Long, “Efficient ISAR Phase Autofocus Based on Eigenvalue Decomposition,” in IEEE Geoscience and Remote Sensing Letters (SCI 二区，IF:4.8), vol. 14, no. 12, pp. 2195-2199, 2017.
12. J. Cai, Y. Song, **Y. Sun** and F. Liu, “Fast ISAR Autofocus Algorithm via Sub-Aperture,” in The Journal of Engineering, vol. 2019, no. 20, pp. 6499-6502, 2019.
13. J. Cai, J. Xu, **Y. Sun** and T. Long, “A Modified ISAR Autofocus Algorithm based on Single Eigenvector,” in International Conference on Radar Systems, Belfast, pp. 1-5, 2017.
14. R. Zhuang, H. Fan, **Y. Sun**, L. Ren and E. Mao, “Pulse-Agile Waveform Design for Nonlinear FM Pulses based on Spectrum Modulation,” in 2020 IET International Radar Conference, 2020.
15. Z. Liu, L. Ren, **Y. Sun**, H. Fan and E. Mao, “Waveform Design of LFM Pulse Train based on Pulse Width Agility,” in 2020 IET International Radar Conference, 2020.
16. 刘子豪, 任丽香, **孙颖豪**, 范花玉, “基于动态规划的捷变脉冲串优化设计方法,” 空军预警学院学报, 2021.
17. 刘泉华, **孙颖豪**, 蔡津剑, 龙腾: 一种基于加窗处理的雷达脉冲压缩输出的副瓣抑制方法, 发明专利, 已授权 CN201810185600.8
18. 刘泉华, **孙颖豪**, 蔡津剑, 龙腾: 一种控制频谱主副瓣特性的加窗方法, 发明专利, 已授权 CN201810339546.8
19. 范花玉, **孙颖豪**, 毛二可, 任丽香: 一种针对雷达波形分集的联合失配滤波器及其设计方法, 发明专利, 已授权 CN201911229038.5
20. 范花玉, **孙颖豪**, 任丽香, 刘泉华, 毛二可: 一种基于距离选通和交替反演的折叠杂波的抑制方法, 发明专利, 已授权 CN202210003864.3
21. 任丽香, 龙腾, 刘子豪, **孙颖豪**, 毛二可, 范花玉: 一种基于脉间相位频谱双捷变的波形设计方法, 发明专利, 已授权 CN202110793850.1
22. 范花玉, 刘子豪, 沙明辉, 毛二可, 任丽香, **孙颖豪**: 一种基于脉宽捷变的 LFM 脉冲串信号波形设计方法, 发明专利, 已授权 CN202110800109.3

## <img alt="honor" src="assets/icon/info-circle-solid.svg" width="30px"> 部分代表性荣誉

- 2023年11月，中国卫星导航定位协会优秀博士学位论文
- 2022年07月，北京市优秀毕业生
- 2022年07月，北京理工大学2022届优秀毕业生
- 2022年06月，北京理工大学优秀博士学位论文
- 2020年12月，国家奖学金（博士研究生）
- 2020年08月，国家公派出国留学资格（新加坡南洋理工大学公费交流一年）
- 2020年07月，北京市三好学生
- 2019年12月，“华为杯”第十六届中国研究生数学建模竞赛，全国二等奖
- 2015年09月，全国大学生电子设计竞赛（北京赛区）三等奖
- 2014年11月，国家奖学金（本科生）
- 2013年12月，第三十届全国部分地区大学生物理竞赛非物理A类，全国二等奖