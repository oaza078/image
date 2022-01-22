## ICA_Readme

### Spec

![imageG(P]TODAVM_QUZB_JA61FH2](C:\Users\hasee\Desktop\imageG(P]TODAVM_QUZB_JA61FH2.png)

### Files

ICA + timer + main

ICA

- ICA用于

timer

- 用于记录时间，返回此步骤用时

main

### Class & Struct

| Name            | Type          | Spec                                                         |
| --------------- | ------------- | ------------------------------------------------------------ |
| Country_Profile | struct        | 重载<，==；含有map Country，double cost                      |
| Country         | map<int, int> | key为country的维度序号，在ParamIndex中按序标号；value为ParamVal中随机抽取的值 |
|                 |               | country是一个N维的map，记录了该国家N维的数据                 |
| Imper_Profile   | struct        | 重载<；Country_Profile Imper，list ColonyList                |



##### class ICA

##### Functions

| Name                        | Parameter                      | Spec                                                         |
| --------------------------- | ------------------------------ | ------------------------------------------------------------ |
| ICA()                       | ...                            | 构造函数，初始化各量，打印日志                               |
| InitializeCountries()       | /                              | 对每一个国家，第key维的量随机在参数表中赋值value；根据国家势力值计算cost，不符合（>=InAcceptableCostVal）就重新抽取，结果压入m_CountryList |
|                             | map<int,int> *Countries, int n | 拷贝前n个Countries给m_CountryList，然后对m_CountryList初始化 |
|                             | list<map<int,int>> Countries   | 拷贝Countries给m_CountryList，然后对m_CountryList初始化      |
| InitializeImpires()         | /                              | 国家按势力排序，前几个国家变成帝国，循环给每个帝国一个殖民地 |
| ColonyCostCalc()            | /                              | 计算每个殖民地的cost                                         |
| Assimilate_Clony_to_Imper() | /                              | 对每个帝国，对该帝国的每个殖民地，随机挑选该势力的某个帝国，将该帝国的value赋值给colony |
|                             |                                |                                                              |
| Doing_Revolution()          | /                              | 革命几率*帝国势力数向下取整即为革命数。随机挑选一个帝国势力，对该势力的每个殖民地势力，随机挑选该势力的两个殖民地国家交换value |
| Colony_Imper_swap()         | /                              | 对每一个帝国势力，对该势力的每个殖民地，若殖民地的cost<帝国的cost，则交换殖民地势力与帝国势力 |
| Eliminate_Weakest_Imper()   | /                              | 帝国势力排序，将最弱帝国的第一个殖民地（若没有殖民地，则将他自己）给最强帝国 |
| Merge_Similar_Impers()      | /                              | 对每一个帝国势力，找到其之后与其cost相等的帝国势力，殖民后者与后者的殖民地 |
| Compet()                    | map<int,int> &Imperialist      | 主函数。初始化                                               |



### Process

1. Initialization

    初始化 Parameter表中的量

    ### Parameters

    | Name                   | Spec                                                         | Type              |
    | ---------------------- | ------------------------------------------------------------ | ----------------- |
    | ParamIndex             | 任意国家势力值的索引值列表                                   | list<int>         |
    | ParamVal               | 可能取到的国家势力值的集合                                   | list<int>         |
    | CountryNum             | 国家的数量                                                   | int               |
    | ImpNum                 | 最初十年帝国的数量                                           | int               |
    | DecadeNum              | 年代数（算法的最大重复次数）                                 | int               |
    | RevolutionRate         | 国家发生革命事件的几率                                       | double            |
    | IsEqualParamValAllowed | 如果每个参数值必须是唯一的，则该参数必须设置为false          | bool              |
    | CostFunc               | 必须返回双精度值的适应度函数地址                             | const Costfuntype |
    | InAcceptableCostVal    | 不可接受的成本函数最大值（如果一个国家的成本值等于或大于它的成本值，其将被消除） | double            |
    | LogfileName            | 日志记录                                                     | string            |

    InitializeCountries();
    
    InitializeImpires();

