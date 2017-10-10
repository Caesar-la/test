---
title: Altizure 的非凡 2016
date: 2016-12-30 00:00:40
tags:
    - 三维应用
    - 三维技术
    - Altizure App
categories:
    - 三维应用
---

2016 年是 Altizure 上线来第一个完整的年份，值得铭记。我们在这一年里推陈出新，锐意进取。在技术上无论是 Altizure.com 的三维重建引擎还是 Altizure App 都获得了长足的进步。同时来至世界各地的热情用户和优质三维作品不停地激励着我们的所有的团队成员。一起来回顾一下 Altizure 的非凡 2016。 

<center>
<iframe src="https://www.altizure.com/project/54ed7ff541fbfa3e1967fc78/model/embed#autoplay=false" style="border:none;width:100%;height:540px"></iframe>
2015 年 Altizure 引擎重建的香港科技大学三维模型
</center>

<center>
<iframe src="https://www.altizure.com/project/583d844035666e6901ec9a33/model/embed#autoplay=false" style="border:none;width:100%;height:540px"></iframe>
2016 年 Altizure 引擎重建的香港科技大学三维模型
</center>


<!-- more -->

# 1. 更好的三维效果

Altizure 自创办之初就定位全三维的数字重建、分享和应用上。我们一直致力于简化三维数据采集的流程，提高三维重建和三维渲染的效果和效率，和丰富三维数据的应用。在过去一年，我们在全流程的每个方向都获得长足的进步，后台三维重建引擎总共进行了 40 次升级。百闻不如一见，我们先看看这一年三维效果的显著提升！

我们先从 Altizure 的第一个在线三维模型 “HKUST Academic Buidling” 来看看这一年来 Altizure 有什么变化。在 HKUST 中的广场里有个红色雕塑，即使用同2015年一样的相片，最新的三维引擎比一年前的引擎可以更好地还原出雕塑的形态。

{% asset_img "hkust-compare-1.jpg" "更加逼真和锐利的纹理，毫不含糊的细节。广场中间的雕塑的细节和形态均可完美呈现。<br><br>左图：2015年引擎生成的结果。右图：2016年引擎生成的结果。" %}

接着我们看看美国旧金山市中心的一个实景三维的改进情况。许多在旧引擎中无法正确重建的楼房模型和扭曲变形的贴图纹理在最新版的引擎里都得到了完美重现。

{% asset_img "city-3-compare-1.jpg" "美国旧金山的实景三维模型细节。<br><br>左图：2015年引擎生成的结果。右图：2016年引擎生成的结果。" %}

下面我们详细介绍一下各项改进。

## 1.1 更鲁邦和高效的空三

从 Altizure 上线来的第一天，我们就致力于提供全自动的三维重建服务，无需任何额外的飞行姿态和相机参数输入，所有相机的位置、姿态、和镜头参数均通过空三自动提取和优化 —— 这个步骤就是空三 (Structure from Motion)。空三提供的相机位置和姿态参数是三维重建的基础中的基础。缺乏空三的成果，就无法把三维模型还原出来。众所周知，传统空三算法在图像数目增长的时候，计算时间会指数级数增长。例如图像数目增长2倍，但时间会变长4倍甚至更多。此外，如何使空三可以在多机器上并行也是一个难题。这导致许多城市级别的航拍数据，需要把图像按照区域分块进行三维重建，这样需要控制点才能把不同区块拼接起来，会导致项目可控性变差，运行效率低。

{% asset_img "sfm-view-1.jpg" "得益于高效鲁邦的空三，我们的系统可以轻松整体处理超过 40000 张图像的三维重建无需控制点和分块。<br><br>上图：整体空三结果。下图：空三结果侧视图，无需控制点亦可还原出平整不分层的飞行轨迹和姿态。" %}

针对这些问题，我们通过机器学习和图像识别的办法，对图像进行识别和分类，大大减少了空三的计算量。并且把传统的串行式空三几何计算升级为并行分布式的计算流程。使得 Altizure 的三维重建引擎在处理城市级别的大规模图像数据时易如反掌。这里我们给大家展示两个城市级别数据量的空三结果 (上下各一个案例)。

{% asset_img "sfm-view-2.jpg" "空三模块能够自动适应不同的飞行载具拍摄。<br><br>直升机航拍，单块数据量超过 50000 张相片，每个拍摄点是8镜头倾斜相机。<br><br>上图：整体空三结果。下图：8 镜头倾斜相机的空三细节。" %}


## 1.2 更精细快速的网格模型重建

新版 Altizure 采用了网格细节优化技术，进一步还原细节，使三维模型更加贴近于真实场景。这无论对视觉效果还是精确计量，都是至关重要的。在优化中，引擎会根据相片中的每个像素调整每个三角面片的位置和朝向，使得每个三角面片均尽可能还原物体的几何形态 (效果见下图)。

{% asset_img "detail-compare-1.jpg" "城堡三维重建的细节优化效果。<br><br>左图：2015年的网格模型。右图：2016年末的网格模型。" %}
{% asset_img "detail-compare-2.jpg" "建筑立面三维重建的细节优化效果。<br><br>左图：2015年的网格模型。右图：2016年末的网格模型。" %}

在实际的航拍中，楼面、屋顶等场景都具有重复纹理 (repetitive) 的特征。如何重建重复纹理的区域，一直来都是三维重建的一大痛点。我们专门对此进行了优化。一般的重建算法（下图左）在重复纹理区域常常错误地重建出现阶梯状的网格模型，而经过优化的 Altizure 引擎可以很好的消除这种错误，呈现出正确、完整的重复纹理结构。重复纹理部分的隆起与塌陷问题也随之消失。屋顶部分的重建自然而逼真。

{% asset_img "detail-compare-3.jpg" "针对重复纹理的优化。<br><br>左图：2015年的模型。右图：2016年末的模型。" %}

> 访问 {% post_link altizure-better-3d-reconstruction-in-the-same-speed 三维重建引擎细节升级 %} 文章了解更多详情。

## 1.3 更简化的网格模型

{% asset_img "sim-compare.jpg" "全新升级模型简化是数据量更小但是依然可以保留逼真的模型细节。<br><br>左图：2015年的网格模型，右图：2016年末的网格模型。" %}

最新的 Altizure 引擎给三维重建得到的网格模型引入了更智能的网格简化 (mesh simplification) 算法，使模型的平面部分更加简化，让平面更加平整，但是细节部分却没有丝毫降低。新的模型简化算法让模型文件大小比原来减小了60%，并带来了以下至关重要的好处：

* 更快的网络加载速度
* 更少的内存消耗
* 更优的 CPU 和 GPU 渲染效率

## 1.4 更自然、更漂亮的纹理贴图

{% asset_img "tex-compare.jpg" "全新升级的贴图算法使得颜色更加自然，过度更加平滑。<br><br>左图：2015年的纹理贴图。右图：2016年末的纹理贴图。" %}

我们采用了新的纹理贴图算法，并加入了自动匀色功能，让不同曝光和白平衡的照片贴图匀成同一色调，使模型纹理看起来更加自然。同时，它也能处理一些因高亮和反射产生的不一致纹理（如上图），让模型整体看起来更加逼真。

## 1.5 更快速和逼真的三维渲染

三维渲染，一直是三维效果呈现的重中之重。Altizure 的在线三维浏览器致力于为您提供流畅的浏览体验，展现丰富、精致的视觉效果。

Altizure 可以从图像重建出高精度的三维模型，一些较大的场景的三角面片数量动辄以亿计。对于这一量级的模型，即便是专业的三维CG软件，也倍感吃力。如何在网页上实时渲染更是业界难题。我们特别研发了场景分解算法，在帧率和视觉效果之间寻求最佳平衡点。在保证顺畅交互的同时，大幅增加了您所能观赏到的细节。Altizure的三维浏览引擎使用这个四两拨千斤的方式，渲染再大规模的模型也可以举重若轻。

{% asset_img "fountain-compare-2.jpg" "左图：旧渲染引擎。右图：新渲染引擎。<br><br>渲染细节比较。注意雕塑的纹理细节。" %}

> 访问 {% post_link 3d-browser-upgrade-stunning-details 三维渲染引擎升级 %} 文章了解更多详情。


# 2. 更智能的航拍图像采集

我们的 App 在过去的一年推出了 21 次重要升级。使用体验得到大幅度的提升。我们为 App 加入了任务参数与飞行进度保存、换电续飞功能，也提供了更丰富的自定义选项。从初版简单的起飞拍照降落，进化到现在更加完整的任务管理。同时 App 内部也进行了多方面的改进，把自动拍照程序、飞行器状态检查和飞行纪录做得更完善，让拍照流程变得更稳定省心。非常感谢所有使用 Altizure App 的朋友们，感谢各位提出的宝贵建议。

这一年，我们的 App 开发团队紧跟着大疆的每一次产品发布，总是迅速投入到新机型的支持中。发布之初，我们还只支持精灵3专业版和悟1，而现在 App 支持大疆 P3, P4, Mavic, 悟和 M600 等大疆全系列无人机，以及 A2, A3, N3 等飞控。近期的 iOS 更新更是使它成为首个支持 Phantom 4 Pro 的第三方 App。下一年，请大家尽情期待新的飞行器。毫无疑问，我们会第一时间为它们提供支持。

{% asset_img "ios-app-compare.jpg" "2016 年带来了更多支持的机型、更安全的飞行和更智能的任务管理。<br><br>上图：2015 年的 iOS App。下图：2016年最新的iOS App 2.6.1" %}

> 访问 {% post_link altizure-better-3d-reconstruction-in-the-same-speed iOS 2.4.3 升级 %} 了解最新 iOS App 的详情。
> 访问 {% post_link altizure-better-3d-reconstruction-in-the-same-speed 安卓 2.6.0 升级 %} 了解最新安卓 App 的详情。


# 3. 更多用户和作品

{% asset_img "visiting-2016.jpg" "用户来自全球超过180个国家和地区。" %}

去年有来自超过180个国家和地区的用户访问 Altizure.com，并且有超过80个国家和地区的三维模型。更多的用户给我们带来了更多精彩的三维作品。这些作品涵盖了超过80个国家和地区，题材百花齐放，古迹，宗教建筑，现代建筑，自然景观，私人别墅等一应俱全。使用的采集设备也是各式各样，有各种品牌的无人机，大疆、零度、eBee，还有各式手机 iPhone，华为，小米，再到传统相机佳能尼康单反，卡片机。借助于 Altizure 强大引擎，所有这些相片，无论是什么题材，什么设备，什么角度拍摄的，均可以进行全自动的三维重建。

我们在这里和大家一起回顾一些 2016 年的经典作品。

## 3.1 经典作品

<center>
<iframe src="https://www.altizure.com/project/57f8d9bbe73f6760f10e916a/model/embed#autoplay=false" style="border:none;width:100%;height:540px"></iframe>
法国巴黎圣母院
</center>

<center>
<iframe src="https://www.altizure.com/project/57c0160d8a8c33464773c6fe/model/embed#autoplay=false" style="border:none;width:100%;height:540px"></iframe>
中国汕头南生大楼
</center>

<center>
<iframe src="https://www.altizure.com/project/579b5c1aea217bf92e2f8e11/model/embed#autoplay=false" style="border:none;width:100%;height:540px"></iframe>
中国长沙橘子洲头毛泽东像
</center>

<center>
<iframe src="https://www.altizure.com/project/567791fe9e0bd5b06ced19ba/model/embed#autoplay=false" style="border:none;width:100%;height:540px"></iframe>
中国深圳滑坡 2015年12月
</center>

<center>
<iframe src="https://www.altizure.com/project/5721f35532f7a5ee26ff0755/model/embed#autoplay=false" style="border:none;width:100%;height:540px"></iframe>
日本熊本地震 2016年4月
</center>

<center>
<iframe src="https://www.altizure.com/project/573db054d75edace1f8c7cc3/model/embed#autoplay=false" style="border:none;width:100%;height:540px"></iframe>
厄瓜多尔地震 2016年4月
</center>

## 3.2 更广泛的企事业合作

2016 年，我们成为南方测绘图像处理云平台的独家技术合作伙伴，为东北和海南两个片区的三维信息服务系统提供自动化三维数据建模服务，未来还有多个大片区建模项目正在实施过程中。下面是一个北方城市的三维重建结果。

{% asset_img "city-1.jpg" "北方某城市三维重建，总共 48283 张相片，约 1200 GigaPixels。全自动三维重建，无需分块，整体一次出成果。" %}
{% asset_img "city-1-zoom.jpg" "北方某城市三维重建。" %}


我们与深圳市勘察研究院有限公司及深圳市武测空间信息有限公司共同助力龙岗中心城智慧城市建设，提供由照片自动生成三维模型的整体解决方案。项目任务重，工期长，数据量极大。其中重点片区的自动化建模任务已完成，在三维效果及生产效率上得到客户的大力认可，目前全区域三维数据生产仍然在紧锣密鼓的进行中。

{% asset_img "city-2-overview.jpg" "南方某城市三维重建，总共 36484 张相片，约 1320 GigaPixels。全自动处理，无需分块，整体一次出成果。" %}
{% asset_img "city-2-zoom.jpg" "南方某城市三维重建的细节。" %}

此外我们在 2016 年还为国内外数十家企事业单位提供了云平台或线下三维数据处理服务，建模成果均得到客户的高度认可。在建模质量、建模效率、易用性这些关键指标上，均强于同类产品。

# 4. 你好 2017

我们坚信一个全三维的数字未来。在 2017 年，我们将致力于提供更加方便、快速、丰富的三维重建技术和应用。感谢所有访问使用 [Altizure.com](https://www.altizure.com) 和支持我们的朋友与同行。祝大家 2017 新年愉快！

---

* 访问 [altizure.com/features](https://www.altizure.com/features) 了解更多 Altizure 的特性
* 访问 [altizure.com/explore](https://www.altizure.com/explore) 浏览更多 Altizure 三维模型
* 下载 Altizure App 控制无人机自动采集照片制作三维模型: [iOS](https://itunes.apple.com/us/app/altizure/id1018791616) / [Android](http://www.wandoujia.com/apps/com.everest.altizure)
* 前往 [Altizure 论坛](https://www.altizure.com/support)，向我们的工作人员和其他伙伴寻求帮助，提出宝贵的建议，帮助我们改善 Altizure

---
小测试