<!--
 * @Date: 2023-03-03 17:04:17
 * @File: 
-->
# 埋点数据的加密

## 功能
为了加强埋点数据的安全性，神策分析支持对埋点数据进行加密，并以密文的形式对数据进行存储和发送。  

## 集成
### 参数说明
- `k`: AES 加密密钥，类型：`string`。
- `kid`: 加密密钥 id，类型：`number`。
- `khash`: 密钥哈希值，类型：`string`。

#### 其他模板集成方式
```javascript
import AesEncryption from '/plugin/encryption/index.esm';
//需要在 init 之前注册插件
sensors.usePlugin(AesEncryption,{
      k:'加密密钥',
      kid: '密钥编号',
      khash: '密钥哈希值'
  });

sensors.init();
```
#### 简易模板集成方式
```javascript
<script charset='UTF-8' src="在 github 下载新版本的 index.amd.js "></script>
<script>
	var AesEncryption = window['sensorsPlugin_AesEncryption'];
	//需要在 init 之前注册插件
  sensors.usePlugin(AesEncryption,{
        k:'加密密钥',
        kid: '密钥编号',
        khash: '密钥哈希值'
    });

  sensors.init();
</script>
```
## 变动
加密后的数据在上报时，通过抓包网络请求栏查看数据消息体中可以看到 payload 或者 payloads 参数，payload 或者 payloads 参数的值为加密后的密文。

## ⚠ 注意
* 本功能需要服务端的配合，可以联系神策客户成功/项目经理协助开通服务端解密功能。
* 加密插件下线时注意事项：  
主 SDK 版本回退至 SDK 版本号 >= 0.1.2 版本时 ，只下线加密插件  
* 开启加密后，如果服务端不支持解密，数据无法入库，会丢失，埋点管理中不会有报错
* 版本要求：
We 码小程序 SDK v.0.1.2 及以上版本   
Edge v0.3.0及以上的版本   
SDF 2.3及以上的版本   
