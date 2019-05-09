# 记录模型对应的训练参数

## 1.simple_spread

test15：用openai之前的reward方式，但是把目标奖励改成了15。这个模型训练的时候用的协作参数，现在这个模型被完全废弃掉，如果要看协作，移步至simple_spread_collaborative这个任务。

testnewrew:重新写了一种reward的方式，完全抛弃了之前的思路，看起来有效果。reward的思路是增加了agent和路标的reach参数，如果agent到达了某个路标，应该维持住，这个其他agent就不应该去找个路标了，而是寻找其他路标。这个任务现在被改装成了3个agent要把3个路标点占据住。但是有个bug是路标的reach参数需要能被读取。（现象好奇怪，怀疑代码有问题）

testnewrew15: 把碰撞reward上调到15**（到55001感觉学出来了，奇怪的是agent一开始会抢夺某个路标，先到的那个其实有时候会被挤走，然后不得不寻找下一个路标，最后一个agent比较难到终点，会出现不动或者rew越来越小的情况，在25001步时会出现两个agent停在一个路标，但是不会有agent放弃这个路标点。最后一个agent的行为看起来没训练好。。，最后一个agent经历两次换目标点之后就跑飞了。）**

## 2.simple_spread_avoid（*可以终止测试了*）**

test:最早能训练出来的模型

testdist:把before去掉

testrew30：把奖励改成了30，碰撞惩罚还是15

结论是没有本质提升，rew改成30之后，对于碰撞的躲避行为减轻了很多。

test4：训练4个agent看一看。其他参数还是15那一套。（250001完全能训练出结果，那么mge那个就相当奇怪了！！！why？难道固定环境的要比随机环境的还难？强制终止）

## 3.simple_spread_mge

test:忘了，但是这个模型就不好使

testbefore:reward里面加了before，同时把距离改成了0.4，探索距离变小了。目前这个模型能看到有两个agent能到达。（结果根本不对，好奇怪，看起来agent根本没见过最优状态 强制终止了）

test2:把agent变成了2个，试一下是不是可以。(可以出结果。。。)

test3:把agent变成3个试试。(稳定成功一个，偶尔两个，三个很罕见)

## 4.simple_spread_collaborative

test：按照openai默认的reward训练，改动15。（完全不对，根本维持不住状态ing 强制终止了，根据状态来说，代码肯定有问题，所以协作参数根本就不能打开，目前来说）

testno：关闭了协作参数试一试**（只有一个或者两个能到，第三个看起来根本不对。。。也留不住）**

testagain:打开协作参数再试一次(还是不行。。。)

## 5.simple_spread_avoid_range

test:增加范围惩罚（3倍的agent半径），两个agent在一定范围内就要惩罚。**（4个agent训练出来了。。。但是避障行为不明显，还是会重叠）**

test5：改成了3个agent，距离惩罚变成了5.**（避障行为学的出来了）**


## 6.simple_adversary
testfalse:reward重新写了（看起来是写错了，用的run2）

## 7.simple_tag
testnew:观测和reward都改了（训练出来了一点东西，有追捕的感觉）

## 8.simple_push
test:观测修改了（怪怪的。。。）


