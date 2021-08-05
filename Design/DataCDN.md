# 资源服务器部署注意事项

## 远程部署的资源
Unity WebGL转换小游戏主要有两个游戏阶段需要下载资源：
- 首资源包
- 按需加载资源

### 首资源包
包含：Unity builtin + 勾选的导出场景 + Resources.

下载方式：小游戏支持“小游戏分包” 与 “CDN”两种方式下载。如果使用“小游戏分包“则需要足够小，因为所有小游戏包体积不能超过20MB。

### 按需加载资源
包含：AB/AA下载的资源，通常使用LZ4压缩。

下载方式：开发者通着需要自行使用CDN服务器进行托管。

## 资源服务器注意事项
1. 针对txt文件进行开启gzip压缩，首资源包有非常高的压缩率
2. CDN服务器开启跨域设置(否则iOS可能会出现跨域加载失败的情况)
3. MP开发者后台为CDN域名添加到"安全域名"
4. 小游戏资源下载并发数为10，超过时底层自动排队
5. 单个请求文件最大不超过100MB，超时默认为60s