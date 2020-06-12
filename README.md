# VERSION 1.2.5 
	增加VIVO支持
	修改头条banner底部位置，防止审核不过
	增加跳转记录处理

# VERSION 1.2.2

	增加了OPPO事件回调
	增加了事件消息系统
	增加了QQ showAppBox 的关闭回调

# VERSION 1.2.0

	增加了头条支持   
	增加了手Q支持   
	修复了若干bug   


## 开发准备 

cocos 使用SDK范例：  http://git.liteplay.com.cn/open/cocos-sdk-demo

微信API地址： https://developers.weixin.qq.com/minigame/dev/api  
微信开发者工具下载： https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html 

头条API地址： https://microapp.bytedance.com/dev/cn/mini-game/develop/api/mini-game/bytedance-mini-game     
头条开发者工具下载：https://microapp.bytedance.com/dev/cn/mini-app/develop/developer-instrument/developer-instrument-update-and-download 


手Q账号注册： https://q.qq.com/#/   
手QAPI地址：https://q.qq.com/wiki/develop/game/API/   
手Q开工具下载：https://q.qq.com/wiki/tools/devtool/   

## 关于广告ID

moosnow.conf.js 中的 banner id, video id, inter id 等广告ID 是需要用账号登录游戏平台申请的

微信广告ID需满足1000个用户
申请地址： https://mp.weixin.qq.com/wxopen/frame?t=promotion/promotion_frame&page=applet/index&token=1153971846#/

联系运营人员协助开通广告ID


## 平台打包说明
    如果你的开发工具没有头条、QQ的打包方式选择，请选择微信模式
    

## 关于统计配置  
### 复制utils 文件夹到你的项目根目录  
在ald-game-conf.js 中配置app_key、configUrl 两个参数，参数由墨雪运营人员提供  
![Image text](http://aldpicsh.aldwx.com/doc_aldwx/xyxtj-wxxyxsdkjr03.png)

## 如果出现运行错误，如下图  
![Image text](https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/SDK/guide/guide_error.jpg)  


## 请将 ald-game.js 移动往下移动几个位置 以COCOS 2.3.3 为例   
![Image text](https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/SDK/guide/guide_error2.png)


# 墨雪SDK使用说明

http://git.liteplay.com.cn/open/moosnowSdk

## 点击下载压缩包  

![Image text](https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/SDK/guide/sdk_guide.png)


## laya使用

将文件moosnow.conf.js、moosnow.platform.sdk.js 拷贝到bin目录

![Image text](https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/SDK/guide/sdk_guide_laya.png?v=2.0.0)

在bin/index.js的文件最后引入文件

```js 

    loadLib("moosnowSdk/moosnow.conf.js")
    loadLib("moosnowSdk/moosnow.platform.sdk.js")
    
```



## Cocos Creator 使用方式
![Image text](https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/SDK/guide/sdk_guide_cocos.png)



## 使用说明



## 配置文件moosnow.conf.js 详解

```js 

    window.moosnowConfig = {
		debug: "wx",//pc时的调试版本 仅仅用来访问接口数据
        wx: { //微信平台
            bannerId: "adunit-e51b3123060eec9e",   //请填写你自己的APP banner id
            videoId: "adunit-a322f5ee40076372",    //请填写你自己的APP video id
            interId: "adunit-7c61767905a3940a", //请填写你自己的APP inter id   
            nativeId: "",
            moosnowAppId: "wx840e2e246968f224",
            version: "1.0.0",
            url: "https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/config/tp_zzxhcar_config.json",
        },
        oppo: { //OPPO平台
            bannerId: "168776",
            videoId: "168781",
            interId: "168777",
            nativeId: ["168779", "168780"],
            moosnowAppId: "30251588",
            version: "1.0.0",
            url: "https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/config/tp_zzxhcar_config.json",
        },
        qq: { //手Q平台
            bannerId: "168776",
            videoId: "168781",
            interId: "168777",
            nativeId: "",
            boxId: "", //qq游戏特有的广告
            moosnowAppId: "30251588",
            version: "1.0.0",
            url: "https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/config/tp_zzxhcar_config.json",
        },
        bd: { //百度平台
            bannerId: "168776",
            videoId: "168781",
            interId: "168777",
            nativeId: "",
            moosnowAppId: "30251588",
            version: "1.0.0",
            url: "https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/config/tp_zzxhcar_config.json",
        },
        byte: { //字节跳动-包含头条、抖音等
            bannerId: "168776",
            videoId: "168781",
            interId: "168777",
            nativeId: "",
            moosnowAppId: "30251588",
            version: "1.0.0",
            url: "https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/config/tp_zzxhcar_config.json",
        }
    }


```

### 第一步 在游戏开始时调用平台登陆


```js 


   moosnow.platform.login(() => {
       console.log('登录成功 ')
   })

```


### 第二步 在游戏Loading结束时


```js 

    moosnow.http.finishLoading();

```


## 游戏版本检查 目前OPPO平台需要使用 微信可以不使用

```js


    /**
     * 检查当前版本的导出广告是否开启
     * @param {string} version 版本号 为了兼容旧版本SDK的参数，目前已无作用，SDK会取moosnowConfig 中的version 来判断
     * @param {*} callback
     * @returns callback回调函数的参数为boolean，true：打开广告，false：关闭广告
     */
    moosnow.platform.checkVersion("1.0.0", (res)=>{
        
    }) 

```




### 获取广告

```js 

    /**
     * 
     */
    moosnow.ad.getAd((res) => {
        console.log('广告数据 ',res)
    })

```

moosnowResult 结构如下图
![Image text](https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com/SDK/guide/sdk_guide_moosnowResult.png)

目前的广告仅有indexLeft数据，其他请忽略




## 广告跳转


```js 

    var btn=new Button();
    /* 跳转传入参数结构
    var navigateData={
        appid:"",
        
        boxAppid:"",
        
        desc:"",
        
        img:"",
        
        path:"",
        
        title:""
    }
    *///导出页 跳转到 第1个app，这个是示例  ， 请根据实际情况填写

    var navigateData=moosnowResult.exportPage[0]
    btn.on("click",function(){
        //将会跳转到navigateData.appid 的小app, 注意！！！ 不要再使用wx.navigateToMiniProgram  
       moosnow.platform.navigate2Mini(navigateData,(res)=>{
           console.log('跳转成功 ',res)
       },(res)=>{
            console.log('跳转失败 ',res)
       })
    })


```



##  微信平台 上报开始游戏，结束游戏  


```js 

    /**
     * 统计开始游戏
     * @param level 关卡数 必须是1 || 2 || 1.1 || 12.2 格式
     */
    moosnow.http.startGame("1")




 	 /**
     * 统计结束游戏
     * @param level 关卡数 必须是1 || 2 || 1.1 || 12.2 格式
     * @param isWin 是否成功
     */
    moosnow.http.endGame("1", true)

```


##  微信平台 上报视频广告数据

```js 
/**
     * 视频统计
     * @param type 0：视频点击 1：视频观看完成
     * @param info 信息 ex:“领取三倍金币”
     * @param level 关卡数	没有请填”0”
     */
    moosnow.http.videoPoint(0, “领取三倍金币”, “1”)
```

注意：点击之后上报一次，type=0，观看完视频后应再上报一次，type=1。





##  微信平台  其他打点

```js 
    moosnow.http.point('分享三倍')
```




## 获取所有配置项

```js 

    moosnow.http.getAllConfig(res => {
        console.log('游戏的所有配置数据 ',res)
    })
```


## 获取误点次数间隔
```js 

    /**
     * 获取误点间隔次数，启动游戏时调用
     * @param callback 回调参数为misTouchNum:int，当misTouchNum=0时关闭误点，
        当misTouchNum=1时，每次都触发误点（即当misTouchNum=n(0除外)时，每	隔n次，触发误点1次）
     */

    var misTouchNum = 0;
    moosnow.http.getMisTouchNum((res) => {
        misTouchNum = res;		//误点次数间隔
    })
```


## 获取位移次数间隔

```js 

    /**
    * 获取位移间隔次数，启动游戏时调用
    * @param callback 回调参数为misTouchPosNum :int，当misTouchPosNum =0时关闭位移误点，
    当misTouchPosNum =1时，每次都触发误点（即当misTouchPosNum =n(0除外)时，每	隔n次，触发位移1次）
    */

    var misTouchPosNum = 0;
    moosnow.http.getMistouchPosNum((res) => {
        misTouchPosNum = res;		//位移次数间隔
    })

```


## 显示平台banner广告

```js 
    
    moosnow.platform.showBanner((isOpend)=>{
		//目前仅支持微信平台
        console.log('用户是否点击了banner ',isOpend)
    });
   
```



## 如果SDK不能满足需求，可以自己管理创建Banner 配置文件中的ID 可以通过如下方式获取
```js 
moosnow.platform.moosnowConfig.bannerId
```



## 隐藏平台banner广告

```js 
    moosnow.platform.hideBanner();
   
```



## 微信平台 自动刷banner，为了提高曝光量，减少点击率，防止被封杀

```js 
    moosnow.platform.showAutoBanner();
   
```


## 显示平台video广告


```js 


    moosnow.platform.showVideo(res => {
        switch (res) {
            case moosnow.VIDEO_STATUS.NOTEND:
                console.log('视频未观看完成 ')
                break;
            case moosnow.VIDEO_STATUS.ERR:
                console.log('获取视频错误 ')
                break;
            case moosnow.VIDEO_STATUS.END:
                console.log('观看视频结束 ')
            default:
                break;
        }
    })
   
```


## OPPO平台特有的 原生广告  下面有一个使用案例提供参考
```js 
    /**
     * 需要用户获取数据后自己来展示在页面上
     * 注意：不要在页面初始化的时候调用，OPPO会提示广告请求太频繁 ，拿不到数据
     */
    moosnow.platform.showNativeAd((row) => {
        if (row && row.imgUrlList && row.imgUrlList.length > 0) {
            cc.loader.load(row.imgUrlList[0], (err, tex: cc.Texture2D) => {
                if (err)
                    return;
                console.log('native img  url ', tex.url)
                let spriteFrame = new cc.SpriteFrame(tex);
                this.logo.spriteFrame = spriteFrame
            })
        }
    });


    /**
     * 当判断用户点击到广告时，调用这个函数
     */
    moosnow.platform.clickNative();

```

## 下面是使用的例子

```js 
import EntityLogic from "../framework/entity/EntityLogic";

const { ccclass, property } = cc._decorator;

@ccclass
export default class NativeAd extends EntityLogic {


    @property(cc.Sprite)
    logo: cc.Sprite = null;

    @property(cc.Sprite)
    btnLeftTop: cc.Sprite = null;

    @property(cc.Sprite)
    btnBottom: cc.Sprite = null;

    willShow(data) {
        super.willShow(data);
        moosnow.platform.showNativeAd((row) => {
            if (row && row.imgUrlList && row.imgUrlList.length > 0) {
                cc.loader.load(row.imgUrlList[0], (err, tex: cc.Texture2D) => {
                    if (err)
                        return;
                    console.log('native img  url ', tex.url)
                    let spriteFrame = new cc.SpriteFrame(tex);
                    this.logo.spriteFrame = spriteFrame
                })
            }
        });


    }
    onShow() {
        this.node.zIndex = 999;
        this.logo.node.on(cc.Node.EventType.TOUCH_END, () => {
            moosnow.platform.clickNative();
        }, this)
    }
    


}

```



## 字节跳动的视频录制
### 开始录制
```js 

    moosnow.platform.startRecord(null,(e)=>{
            console.log('是否是抖音', e)
    });

```


### 视频精彩剪切（可选）

```js 
    //记录精彩的视频片段，调用时必须是正在录屏，以调用时的录屏时刻为基准，指定前 2 秒，后 2 秒为将要裁剪的片段，可以多次调用
    
    moosnow.platform.clipRecord();



```


### 停止录制
```js 

     moosnow.platform.stopRecord((res) => {
        if (res.videoPath) {
            //录制的视频路径
            this.videoPath = res.videoPath;

            // setTimeout(() => {
            //     this.shareRecord();
            // }, 200);
        }
    });

```
### 分享录制的视频 
```js 
    //这个是默认的分享，如果有特别需求，可以自己调用头条API
	//分享视频是录屏必须已经停止 
	//moosnow.platform.stopRecord((res) => {
    //    if (res.videoPath) {
    //        //录制的视频路径
    //        this.videoPath = res.videoPath;

    //        moosnow.platform.share({
	//			channel: moosnow.SHARE_CHANNEL.VIDEO
	//		}, (res) => {
	//			console.log('分享结束', res)
	//		});
    //   }
    //});
	
    moosnow.platform.share({
        channel: moosnow.SHARE_CHANNEL.VIDEO
    }, (res) => {
        console.log('分享结束', res)
    });

```

## 关于平台判断 SDK做了一套平台判断的方法，属于精准判断
## 在PC调试阶段会受 moosnow.conf.js 中的 debug 的影响

```js 


    let curPlatform = moosnow.getAppPlatform();
    //头条
    if (curPlatform == moosnow.APP_PLATFORM.BYTEDANCE)
    {

    }
    //OPPO
    if (curPlatform == moosnow.APP_PLATFORM.OPPO||curPlatform == moosnow.APP_PLATFORM.OPPO_ZS)
    {

    }
    //QQ
    if (curPlatform == moosnow.APP_PLATFORM.QQ)
    {

    }
    //WX
    if (curPlatform == moosnow.APP_PLATFORM.WX)
    {

    }


```


## QQ平台的盒子广告
```js
    /**
    * 盒子广告
    * @param callback 关闭回调
    * @param remoteOn 被后台开关控制  一般首页传 false  需要误触的地方传true
    */
    moosnow.platform.showAppBox((res) => {
            //res ==-1 表示后台没有开启功能  res==0 表示用户主动关闭了盒子
            console.log('关闭盒子')
    },false);
    
```




## 微信平台   在微信管理后台（ https://mp.weixin.qq.com  ）-->开发-->开发设置-->服务器域名 配置安全域名
```js 

https://api.liteplay.com.cn
https://liteplay-1253992229.cos.ap-guangzhou.myqcloud.com
https://cdn.liteplay.com.cn
https://glog.aldwx.com
https://log.aldwx.com

```
### 复制这里更快噢
```js 
api.liteplay.com.cn
cdn.liteplay.com.cn
glog.aldwx.com
liteplay-1253992229.cos.ap-guangzhou.myqcloud.com
log.aldwx.com
```
