---
description: LDB 详情页面的 PRD
---

# LDB detail page PRD

## 页面原型

![](../../.gitbook/assets/ldb-detail-page%20%283%29.png)

{% tabs %}
{% tab title="1.0" %}
* 1.1 [LDB 图片](./#2-5d-jian-zhu-tu-1-1)
* 1.2[ LDB 名称](./#ldb-ming-cheng-1-2)
* 1.3 [LDB 经纬度](./#zuo-biao-1-3)
* 1.4 [LDB 地址](./#di-zhi-1-4)
* 1.5 [LDB 类型](./#lei-xing-1-5)
* 1.6 [LDB 描述](./#miao-shu-1-6)
{% endtab %}

{% tab title="2.0" %}
* 2.1 [LORD 头像](./#lord-tou-xiang-2-1)
* 2.2 [LORD 昵称](./#lord-ni-cheng-2-2)
* 2.3 [LORD 地址](./#lord-di-zhi-2-3)
{% endtab %}

{% tab title="3.0" %}
* 3.1 [当前售价](./#ldb-shou-jia-3-1)
* 3.2 [出售过期时间](./#jiao-yi-sheng-yu-shi-jian-3-2)
* 3.3 [购买行为](./#zhuang-tai-pan-duan-3-0)
{% endtab %}

{% tab title="4.0" %}
* 4.1 [当前任务](./#dang-qian-ren-wu-4-1)
* 4.2 [领取糖果](./#ling-qu-tang-guo-4-2)
* 4.3 [已完成任务](./#yi-wan-cheng-ren-wu-4-3)
{% endtab %}

{% tab title="5.0" %}
* 5.0 [交易历史](./#jiao-yi-li-shi-5-0)
{% endtab %}
{% endtabs %}

## 功能结构

![](../../.gitbook/assets/ldb-mo-kuai%20%281%29.png)

## 元素与内容

### LDB \[1.0\]

基于现实世界建筑在虚拟世界中的映射。是基于 ETH 的 ERC-721 资产，糖果分发的载体。

#### 2.5D 建筑图 \[1.1\]

此图片为现实建筑 2.5D 化后的绘制图片。

* 格式：PNG/SVG
* 不为空

#### LDB 名称 \[1.2\]

建筑在现实世界中的名字

* 不为空

#### 坐标 \[1.3\]

建筑在现实世界中的经纬度坐标，由 x, y 组成

* 小数
* 不为空

{% hint style="warning" %}
保留小数点后 6 位。
{% endhint %}

#### 地址 \[1.4\]

建筑在现实世界中的地址。

{% hint style="info" %}
目前仅开放上海市，只需显示「区」以后的详细地址。
{% endhint %}

#### 类型 \[1.5\]

建筑的种类目前包括：

* 风景名胜
  * 公园
  * 游乐场
  * 寺庙
* 地铁站
* 著名建筑
* 普通小区

{% hint style="info" %}
著名建筑往往指全国或世界范围闻名遐迩的建筑，如「东方明珠」这类建筑划分到「风景名胜」分类本质上也是可行的。但在 LORDLESS 中更倾向于将其划分入「著名建筑」。
{% endhint %}

#### 描述 \[1.6\]

建筑在真实世界中的评价、历史和描述

### LORD \[2.0\]

LDB 的所有者。

#### LORD 头像 \[2.1\]

依照 LORD 注册时，绑定的 Ethereum 地址生成的抽象化图片。

#### LORD 昵称 \[2.2\]

LORD 在注册时为 Ethereum 地址关联的昵称。

#### LORD 地址 \[2.3\]

用户固有的 Ethereum 地址，在 LORDLESS 中的唯一标识。

{% hint style="warning" %}
只显示前 6 位数与后 6 位，中间部分用「星号」代替。
{% endhint %}

### 交易 \[3.0\]

交易功能描述了当前 LDB 的价格、可交易剩余时间。

#### 状态判断 \[3.0\]

```javascript
if (未出售 && (未登录 || (已登录 && 非 owner))) {
	case 1	// nothing
} else if (未出售 && 已登录 && owner) {
	case 2	// sale	
} else if (已出售 && 已登录 && owner) {
	case 3	// cancel sale
} else if (已出售 && 已登录) {
	case 4	// buy
} else {
	case 5	// sign to buy
}
```

{% tabs %}
{% tab title="Case 1" %}
隐藏不显示该功能视图
{% endtab %}

{% tab title="Case 2" %}
![Sale](../../.gitbook/assets/image%20%285%29.png)
{% endtab %}

{% tab title="Case 3" %}
![Cancel sale](../../.gitbook/assets/image%20%287%29.png)
{% endtab %}

{% tab title="Case 4" %}
![Buy](../../.gitbook/assets/image%20%282%29.png)
{% endtab %}

{% tab title="Case 5" %}
![Sign to buy](../../.gitbook/assets/image%20%281%29.png)
{% endtab %}
{% endtabs %}

#### LDB 售价 \[3.1\]

LORD 选择在交易市场中出售当前 LDB 的价格。

{% hint style="warning" %}
使用千分符
{% endhint %}

#### 交易剩余时间 \[3.2\]

在交易市场出售 LDB 并不是永久上架的，此处显示当前 LDB 在交易市场中的剩余时间。

#### 状态判断 \[3.2\]

|  | _**剩余10天以上**_ | _**剩余10天 - 1天（包括10天）**_ | _**剩余1天以内（包括1天）**_ |
| --- | --- | --- |
| **颜色** | 普通色 | 缓和色 | 紧急色 |
| 格式 | 年/月/日 | 日/时 | 时/分 |

### 任务 \[4.0\]

#### 当前任务 \[4.1\]

当前 LDB 能提供给用户可领取的列表。

#### **状态判断 \[4.1\]**

```javascript
if (建筑有剩余任务数 && (未登录 || (登录 && 非 owner && 用户剩余该任务))) {
	case 1	// show
} else {
	case 2	// hide
}
```

{% tabs %}
{% tab title="Case 1" %}
显示列表
{% endtab %}

{% tab title="Case 2" %}
隐藏列表
{% endtab %}
{% endtabs %}

#### 领取糖果 \[4.2\]

当前 LDB 剩余可以由用户直接领取的糖果数。

#### 状态判断 \[4.2\]

```javascript
var prop = 剩余份数/总份数
```

|  | prop &gt; 50% | 50% &gt;= prop &gt;10% | prop &lt;= 10% | prop = 0 |
| --- | --- |
| 字色 | 普通色 | 缓和色 | 紧急色 | 不可用色 |

#### 已完成任务 \[4.3\]

显示当前登录用户在当前 LDB 中完成过的任务。

{% hint style="warning" %}
* 获取 Candy 数、获取经验使用千分符
* 完成时间只显示到年、月、日、时、分中的最大单位，如：3 年前、5 分钟前
{% endhint %}

#### **状态判断 \[4.3\]**

```javascript
if (登录 && 完成过任务) {
	case 1	// show
} else {
	case 2	// hide
}
```

{% tabs %}
{% tab title="Case 1" %}
显示列表
{% endtab %}

{% tab title="Case 2" %}
隐藏列表
{% endtab %}
{% endtabs %}

### 交易历史 \[5.0\]

当前 LDB 的所有历史交易记录。

#### **状态判断 \[5.0\]**

|  | 天数 &gt; 7 | 7 天 &gt;= prop &gt;0 |
| --- | --- |
| 交易天数字色 | 普通色 | 紧急色 |

{% tabs %}
{% tab title="有过交易" %}
显示列表
{% endtab %}

{% tab title="无交易" %}
官方首次拍卖，无列表显示
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
* 如果卖方地址为 LORDLESS 官方，则直接显示「官方拍卖」
* 只显示前 6 位数与后 6 位，中间部分用「星号」代替。
{% endhint %}





