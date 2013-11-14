#接口定义


### 基本约定

 * 请求方式：***POST***
 * 返回结果：***JSON***

> - 所有请求必须提供 PC_SOCKET=8fabfaaca0cf2afd29ef9365845b322a 这个参数作为验证。
> - 所有参数区分大小写。
> - <应用地址> 目前为内部地址 192.168.0.253/zhushou，请直接代入。其他基本固定。


### 列出 App 分类数据

- 地址
> http://`<应用地址>`/Pcwebservice/`apptype`

- POST 参数说明
> 暂无，直接请求即可。

- JSON 返回说明
> - `Result` - 值为 *true* 表示正确返回数据；
> - `Data` - 数据集合。字段定义如下：
>  - `id` 为分类 id，对应其他接口的 Type 参数
>  - `name` 为分类名称
>  - `pid` 为上级分类。
```
{
    "Result": true,
    "Data": [
        { "id": 1, "name": "\u5e94\u7528", "pid": 0, "flag": 0 },
        { "id": 2, "name": "\u6e38\u620f", "pid": 0, "flag": 1 },
        ...
        ]
}
```


### 获取指定 App 的详细信息

- **接口**
> http://`应用地址`/Pcwebservice/`appinfo`

- **参数**
> `AppId` - 指定 App 的 id；可以单个或者多个，用逗号 `,` 分隔多个。例如 `AppId=1,2,3`。

- **返回**
> - `Result` - 值为 true 表示正确返回数据；
> - `NumData` - 返回数据的个数。
> - `Data` - Data 为数据集合。

- **样例**
```json
{
    "Result": true,
    "NumData": 3,
    "Data": [
        { "id": 1, "name": "QQ", ... },
        ...
    ]
}
```


### 获取 App 列表（1推荐，2好评，3装机必备，4最新，5热门）

- 地址
> http://`应用地址`/Pcwebservice/`applist`

- POST 参数说明
> - `Type` - 分类，int 型。0 默认为不限分类。具体可通过 apptype 方法获取具体分类。
> - `Ptype` - 父分类，1 为应用，2 为游戏，默认为 1 应用。
> - `Dev` - 设备类型，1 为 iPhone，2 为 iPad，默认为 1。
> - `Order` - 排序方式，1 推荐，2 为按好评，3 必备，4 为最新，5 为热门；默认为 1。
> - `PageSize` - 分页大小。即每次获取多少个数据。
> - `Page` - 获取第几页数据。从 1 开始。

- JSON 返回
> - `Result` 值为 *true* 表示正确返回数据。
> - `Total` 符合条件的数据总数，
> - `NumData` 本次返回数据数量，
> - `PageSize` 本次分页大小；
> - `CurPage` 当前页面；
> - `Data` 为数据集合。
```
{
    "Result": true,
    "Total": 8677,
    "NumData": 4,
    "PageSize": 4,
    "CurPage": 2,
    "Type": 0,
    "Ptype": 0,
    "Dev": 2,
    "Data": [{...},...]
}
```


### 获取 App 排行 (1周排行榜，2月排行榜，3.总排行榜)

- 地址
> http://`应用地址`/Pcwebservice/`ranking`

- POST 参数
> - `Type` - 分类。默认为不限分类。可通过 `apptype` 方法获取具体分类信息。
> - `Ptype` - 父分类：1 为应用，2 为游戏，默认为应用。
> - `Dev` - 设备类型：1 为 iPhone，2 为 iPad，默认为 1。
> - `Ranking` - 排行类型：1 周排行榜；2 月排行榜；3 总排行榜。
> - `PageSize` - 分页大小。即每次获取多少个数据。默认为 24。
> - `Page` - 获取第几页数据。

- JSON 返回
> - `Result` 值为 *true* 表示正确返回数据；
> - `Total` 符合条件的数据总数；
> - `NumData` 本次返回数据数量；
> - `PageSize` 本次分页大小；
> - `CurPage` 当前页面；
> - `Data` 为数据集合。
```json
{
    "Result": true,
    "Total": 8677,
    "NumData": 4,
    "PageSize": 4,
    "CurPage": 2,
    "Type": 0,
    "Ptype": 0,
    "Dev": 2,
    "Data": [
        { ... },
        ...
    ]
}
```


### 相关应用推荐

- 地址
> http://`应用地址`/Pcwebservice/`related`

- POST 参数
> - `AppId` - 指定关联的 AppId。

- JSON 返回
> - `Result` 值为 *true* 表示正确返回数据。
> - `AppId` 为请求时指定的 Id 相同。
> - `NumData` 返回数据个数。目前固定返回 8 个。
> - `Data` 数据格式与获取 App 列表接口相同。
```json
{
    "Result": true,
    "AppId": 30,
    "NumData": 8,
    "Data": [ { ... } ]
}
```


### 获取意见反馈数据

- 地址
> http://`应用地址`/Pcwebservice/`suggest_get`

- POST 参数
> - `PageSize` - 分页大小。即每次获取多少个数据。默认为 24。
> - `Page` - 获取第几页数据。

- JSON 返回
> - `Result` 值为 *true* 表示正确返回数据；
> - `Total` 符合条件的数据总数；
> - `NumData` 本次返回数据数量；
> - `PageSize` 本次分页大小；
> - `CurPage` 当前页面；
> - `Data` 为数据集合。
```
{
    "Result": true,
    "Total": 30,
    "NumData": 4,
    "PageSize": 4,
    "CurPage": 4,
    "Data": [ { ... }, ... ]
}
```


### 提交意见反馈数据

- 地址
> http://`应用地址`/Pcwebservice/`suggest_put`

- POST 参数
> - `Title` - 标题。
> - `Content` - 内容正文。
> - `Username` - 用户名。
> - `Email` - 邮件地址。

- JSON 返回
> - `Result` - 值为 *true* 表示提交成功，*false* 或者其他情况表示提交失败。
```
{
    "Result": true
}
```


### App 搜索接口

- 地址
> http://`应用地址`/Pcwebservice/`search`

- POST 参数
> - `Type` - 分类，int 型。0 默认为不限分类。具体可通过 `apptype` 方法获取具体分类。
> - `Ptype` - 父分类，1为应用，2为游戏，默认为应用；
> - `Dev` - 设备类型，1为iPhone，2为iPad，默认为1；
> - `Keyword` - 搜索关键词

- JSON 返回
> - `Result` 值为 *true* 表示正确返回数据。
> - `Total` 搜索结果的总数，
> - `Data` 为搜索结果的 id 数组。
```
{
　　    "Result": true,
　　    "Total": "33",
　　    "Type": "0",
　　    "Ptype": "0",
　　    "Dev": "0",
　　    "Data": [
　　        "438",
　　        "597",
　　        ...
　　    ]
}
```