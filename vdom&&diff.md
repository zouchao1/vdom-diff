##### virtual dom

1.virtual dom即虚拟dom,一个虚拟DOM(元素)是一个一般的js对象, 准确的说是一个对象树(倒立的)。虚拟DOM保存了真实DOM的层次关系和一些基本属性，与真实DOM一一对应,如果只是更新虚拟DOM, 页面是不会重绘的

2.本质：就是在 JS 和 DOM 之间做了一个缓存。

3.https://www.aliyun.com/jiaocheng/977973.html

#### diff算法

1.diff的实现过程就是 patch(container, vnode) 和 - patch
（diff算法是通过同层的树节点进行比较而非对树进行逐层搜索遍历的方式,所以时间复杂度只有O(n),是一种相当高效的算法。）

2.diff的实现的核心就是 createElement 和 updateChildren

3.patch(container, vnode)
        初始化加载，直接将 vnode 节点打包渲染到一个空的容器 container 中


        patchVnode的规则是这样的:

        <1>.如果新旧VNode都是静态的,同时它们的key相同(代表同一节点),并且新的VNode是clone或者是标记了once(标记v-once属性,只渲染一次),那么只需要替换elm以及componentInstance即可。

        <2>.新老节点均有children子节点,则对子节点进行diff操作,调用updateChildren,这个updateChildren也是diff的核心。

        <3>.如果老节点没有子节点而新节点存在子节点,先清空老节点DOM的文本内容,然后为当前DOM节点加入子节点。

        <4>.当新节点没有子节点而老节点有子节点的时候,则移除该DOM节点的所有子节点。

        <5>.当新老节点都无子节点的时候,只是文本的替换。

4.diff算法做了哪些事：

        节点的新增和删除

        节点重新排序

        节点属性、样式、事件绑定

        如何极致压榨性能

    ... ...
5.判断两个VNode节点是否是同一个节点,需要满足以下条件
        key相同
        tag(当前节点的标签名)相同
        isComment(是否为注释节点)相同
        是否data(当前节点对应的对象,包含了具体的一些数据信息,是一个VNodeData类型,可以参考VNodeData类型中的数据信息)都有定义
        当标签是<input>的时候,type必须相同 












