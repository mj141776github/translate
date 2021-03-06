# 项目的由来
最近倒是进了一些群，发现很多人对规则的转换都不是很了解，之前我都是自己写个脚本自己运行一下，就删除了，后来看到了[这个项目](https://github.com/ne1llee/v2ray2clash)，感觉很不错，不过这个老哥支持的不多，我个人喜欢使用命令行生成配置文件直接导入的方式，于是这个版本暂时只支持了命令行方式，web订阅后期再进行开发

这个项目也有一些借鉴了[@ne1llee](https://github.com/ne1llee)老哥的代码，其中makefile我就直接抄了过来，要是老哥觉得不合适，可与我联系
# 功能
- [X] 命令行版本
- [X] web版本 ~~(关于web订阅一直没有开始：web订阅很多app都不允许修改，很不爽啊，我还是喜欢用文本导入，还可以自定义规则)~~ 终于做好啦~
- [X] 支持多订阅链接
- [X] 支持喵帕斯订阅提取v3节点
- [X] 将`v2ray`加入到`神机规则`中（clash）
- [X] 将`ss`加入到`神机规则`中（clash）
- [X] 将`v2ray`加入到`神机规则`中（surge）
- [X] 将`ss`加入到`神机规则`中（surge）
- [X] 将`v2ray`加入到`神机规则`中（quantumultx）
- [X] 将`ss`加入到`神机规则`中（quantumultx）
- [X] 交互式终端操作
- [ ] 黑白名单功能
- [ ] web版本订阅增加账户认证

...

# 使用方法
* 从[release](https://github.com/HarryWang29/translate/releases)下载二进制文件
* 解压相应版本的压缩包
* 多订阅链接直接提供多`--subLink=""`标签即可，样例如下
    ```bash
    ./translate-darwin-amd64 vmess clash --subLink="订阅链接1" --subLink="订阅链接2"
    or
    ./translate-darwin-amd64 vmess clash --subLink="订阅链接1,订阅链接2"
    ```
 * 喵帕斯节点过滤功能，现在只支持vmess协议的订阅，增加`--npsboost`标签，样例如下：
    * 获取喵帕斯v2ray订阅链接为`link1`
    * 获取喵帕斯ssr订阅链接为`link2`
    * 将`link2`中`mu=1`更改为`mu=0`为`link3`
    * 组成命令为
        ```bash
        ./translate-darwin-amd64 vmess clash --subLink="link1" --npsboost="link3"
        ```
    * 注意，喵帕斯过滤功能无法和多订阅一起使用，此功能会按照ss订阅来过滤节点，会将第二个机场的所有节点全部过滤
    
    
## 非终端使用
喜大普奔，增加了终端交互方式使用，现无论mac/windows/linux中皆可双击使用(win10需要双击`run.bat`)，若双击无效，需要增加可执行权限
```bash
sudo chmod 766 translate-darwin-amd64 
```
## 终端使用方式

### 交互式功能
```bash
sudo chmod 766 translate-darwin-amd64 
./translate-darwin-amd64
```
根据终端提醒数据即可：
```bash
请输入想要启动的方式(web/ss/vmess):ss
请输入目标程序(clash/surge3):surge3
请输入订阅链接(多订阅使用','分割:url1,url2):订阅链接
```

### mac/linux
* 执行如下命令修改可执行权限
    ```bash
    sudo chmod 766 translate-darwin-amd64
    ```
* 执行如下命令将v2ray转为clash(保留双引号)
    ```bash
    ./translate-darwin-amd64 vmess clash --subLink="订阅链接"
    ```
* 执行如下命令将v2ray转为surge3(保留双引号)
    ```bash
    ./translate-darwin-amd64 vmess surge3 --subLink="订阅链接"
    ```
* 执行如下命令将v2ray转为quantumultx(保留双引号)
    ```bash
    ./translate-darwin-amd64 vmess quantumultx --subLink="订阅链接"
    ```
* 执行如下命令将ss转为clash(保留双引号)
    ```bash
    ./translate-darwin-amd64 ss clash --subLink="订阅链接"
    ```
* 执行如下命令将ss转为surge3(保留双引号)
    ```bash
    ./translate-darwin-amd64 ss surge3 --subLink="订阅链接"
    ```
* 执行如下命令将ss转为quantumultx(保留双引号)
    ```bash
    ./translate-darwin-amd64 ss quantumultx --subLink="订阅链接"
    ```

### windows
* 双击`run.bat`

## web订阅方式(发版匆忙，若有问题，欢迎打脸)
### 启动命令
```bash
./translate-darwin-amd64 web [--port=8829] [--subLink="订阅链接"]
```
* `[]` 符号代表选填
* `--port` 服务器监听端口，默认`8829`，不填写则使用默认参数
* `--subLink` 启动时默认输入订阅url，会记录缓存，支持多订阅链接，此处订阅链接**不可进行urlencode**

### url请求
```url
http://127.0.0.1:8829/translate?from=vmess&to=clash[&subLink=link1&subLink=link2]
```
* `[]` 符号代表选填
* `from`来源订阅协议
* `to`目标转换软件
* `subLink` 支持多订阅链接，不会记录缓存，每次都必须填写，此处订阅链接**必须进行urlencode**

### 公共网络服务
```url
https://translate.harrywrz.com/translate?from=vmess&to=clash&subLink=urlencode
```

### 样例（语文不好，怕解释不清楚）
* 使用终端传入订阅链接
    * 启动命令
        ```bash
        ./translate-darwin-amd64 web --port=1111 --subLink="link1"
        ```
    * url 调用3
        ```url
        http://127.0.0.1:1111/translate?from=vmess&to=clash
        ```
    * 如上调用每次请求都会获得link1的订阅信息+神机规则-->clash
    
* 使用web传入订阅链接
    * 启动命令
        ```bash
        ./translate-darwin-amd64 web --port=1111 
        ```
    * url 调用2
        ```url
        http://127.0.0.1:1111/translate?from=vmess&to=clash&subLink=link2
        ```
    * 如上调用每次请求都必须传入`subLink`参数，获得link2的订阅信息+神机规则-->clash
    
* 使用终端+web传入订阅链接
    * 启动命令
        ```bash
        ./translate-darwin-amd64 web --port=1111 --subLink="link3"
        ```
    * url 调用1
        ```url
        http://127.0.0.1:1111/translate?from=vmess&to=clash&subLink=link4
        ```
    * url 调用2
        ```url
        http://127.0.0.1:1111/translate?from=vmess&to=clash&subLink=link5
        ```
    * 如上调用1，会获得link3+link4+神机-->clash
    * 如上调用2，会获得link3+link5+神机-->clash

* **_终端传入的`subLink`会被保留在缓存中，后期每次请求都会自动获取最新节点信息_**

# 关于测试
> 个人项目测试案例较少，测试资源较少，若有问题多多包涵，欢迎打脸
>
> 有老哥提醒我ss格式非常混乱，我这里样本较少，若有遇到无法成功订阅的情况，麻烦脱敏后提供格式

已测试机场订阅:
* dler(ss/vmess)
* 喵帕斯(vmess)
* 极游得(热心网友提供)(vmess)

# 感谢
* [神机规则](https://github.com/ConnersHua/Profiles/tree/master)
* [ne1lle](https://github.com/ne1llee/v2ray2clash)
* 墙外不是法外