这个版本是7.26日新建, 是2000个workers的多进程版本，实验多次使得画出来的图像更加的符合规律
可信的worker是定义为
设置20轮的真实值，都是基于the diabetes dataset，
对于每一轮的真实值的操作是把the diabetes dataset进行一定范围的波动生成，
例如是加减10%。
对于指定的worker，需要设置这个worker每轮的属性和地点信任度不变。
指定属性误差度为a, 指定地点误差度为b，则指定地点指定属性原来数据是100，
此worker数据的生成就是100*（1+(-)a%）*(1+(-)b%)。
可信的workers属性和地点误差度都在0.05-0.2之间，中等的是0.2-0.4，不可信的是0.4-0.6.
上面三种的比例分别为 0.6:0.2:0.2
这边的误差度是可以为正可以为负数，比如说某属性误差为0.15,地点误差度为0.1，
成为负数或者正数的比例为0.1
则某个entry的值可以为:
真实值*1.15*1.1; 真实值*0.85*1.1; 真实值*1.15*0.9; 真实值*0.85*0.9

设置有2000个workers，总共200个地点的任务，每个地点的任务关注的属性不一定相同，
意味着有部分地方的属性UAV是不会进行采集的。

代码注意事项: 含有地点的list，像从arrangement的df变化过来的时候，需要变成整数map一下，这里面的列和地点名字是一样的
这边读取csv文件和.columns的时候，列名都是变成了字符串'0'这种
