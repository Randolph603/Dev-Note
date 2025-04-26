# Tencent CloudBase TCB

腾讯云提供的云原生一体化开发环境和工具平台。可用于云端一体化开发多种端应用(小程序，公众号，Web应用等)。包括云数据库(非关系型)，云储存，云函数等功能。

产品基本文档：https://cloud.tencent.com/document/product/876

TCB 控制台：https://cloud.tencent.com/login

## SDKs

There are five types SDKs designed for connecting TCB

1. Web SDK

NPM: [@clouldbase/js-sdk](https://www.npmjs.com/package/@cloudbase/js-sdk?activeTab=readme) is purely JavaScript based libaray.  

> There are two mainly version of package to use V1 and V2.  From the [github](https://github.com/TencentCloudBase/cloudbase-js-sdk/tree/master) source code, it is easy to see that v1 is master branch while v2 is feature/support_oauth2. V2 is still under developing. 

V1 Doc: https://docs.cloudbase.net/api-reference/webv2/initialization

V2 Doc: https://docs.cloudbase.net/api-reference/webv3/initialization

>跨端开发：@cloudbase/js-sdk 只支持常规 Web 应用（即浏览器环境）的开发，不兼容其他类 Web 平台，比如微信小程序、快应用、Cocos 等。

EABC website is using js sdk for website talking to TCB.

2. Wechat App SDK

微信小程序的 SDK，已经直接内置到微信小程序运行框架内，无需额外引用，节省空间。通过微信小程序 SDK，您可以在微信小程序中直接访问 CloudBase 的服务。在开发过程中，请在微信开发者工具中，单击工具菜单中的设置，在项目设置 > 本地设置 > 调试基础库中选择2.2.3或以上版本。

> 海外主体小程序不允许创建TCB云开发，也不允许使用Wechat App SDK去连接TCB。

3. Node.js SDK

[Cloudbase Server Node.js SDK](https://www.npmjs.com/package/@cloudbase/node-sdk) 让您可以在服务端（例如腾讯云云函数或云服务器等）使用 Node.js 服务访问 TCB 的服务，例如云函数调用，文件上传下载，数据库集合文档操作等，方便快速搭建应用。

😶‍🌫️ @cloudbase/node-sdk is the official Node.js SDK provided by Tencent CloudBase (TCB) for server-side development. It allows developers to interact with Tencent CloudBase services programmatically using Node.js. This SDK is particularly useful for backend applications, such as cloud functions or server environments, to perform operations like:

> - Cloud Function Invocation: Trigger and manage cloud functions.
> - File Management: Upload, download, and manage files in Tencent CloudBase storage.
> - Database Operations: Perform CRUD operations on CloudBase's NoSQL database collections.
> - Authentication: Manage user authentication and access control.

🔑 Key Features:
- Designed for server-side environments like Tencent Cloud Functions or custom servers.
- Provides APIs for seamless integration with Tencent CloudBase services.
- Simplifies backend development by abstracting complex operations.

文档：https://docs.cloudbase.net/api-reference/server/node-sdk/introduction

4. Node.js SDK (Manager)

云开发 manager-node sdk ([NPM](https://www.npmjs.com/package/@cloudbase/manager-node)) 支持开发者通过接口形式对云开发提供的云函数、数据库、文件存储等资源进行创建、管理、配置等操作。

5. Open API

Cloudbase Open API allows developers to invoke CloudBase services as an administrator via HTTP requests. This API provides a flexible way to manage and interact with CloudBase resources programmatically, enabling operations such as:

- Managing cloud functions
- Accessing and manipulating databases
- Handling file storage
- Configuring environment settings

Documentation: [Cloudbase Open API](https://docs.cloudbase.net/api-reference/openapi/introduction)

Some key endpoints of API that relative to login and credentials

1. code2Session 小程序登录
https://developers.weixin.qq.com/miniprogram/dev/OpenApiDoc/user-login/code2Session.html

2. getAccessToken 获取接口调用凭据
https://developers.weixin.qq.com/miniprogram/dev/OpenApiDoc/mp-access-token/getAccessToken.html

3. getStableAccessToken 获取稳定版接口调用凭据
https://developers.weixin.qq.com/miniprogram/dev/OpenApiDoc/mp-access-token/getStableAccessToken.html


## Wechat App (Oversea Development)

Due to policy of Wechat Mini Programs oversea, wechat app SDK could not be used directly. The only way to implment is Web SDK @cloudbase/js-sdk. 

And here need to introduce another lib 
**cloudbase-adapter-wx_mp**. It is an adapter provided by Tencent CloudBase (TCB) for integrating the CloudBase JavaScript SDK (@cloudbase/js-sdk) with WeChat Mini Programs. It allows developers to use the CloudBase Web SDK in the WeChat Mini Program environment by bridging compatibility issues between the two platforms.


>🔑 Key Features:
>- Enables the use of @cloudbase/js-sdk in WeChat Mini Programs.
>- Provides seamless integration with Tencent CloudBase services, such as database operations, file storage, and authentication, within the WeChat Mini Program ecosystem.
>- Simplifies cross-platform development by allowing developers to reuse code written for the Web SDK in WeChat Mini Programs.

Usage Example from offical:

``` js
import cloudbase from '@cloudbase/js-sdk';
import wx_mp from 'cloudbase-adapter-wx_mp';

// Initialize the adapter
cloudbase.useAdapters(wx_mp);

// Initialize CloudBase
const app = cloudbase.init({
  env: 'your-environment-id', // Replace with your CloudBase environment ID
});

// Example: Accessing the database
const db = app.database();
db.collection('your-collection').get().then(res => {
  console.log(res.data);
});
```

Best Practice from usage

``` js
import cloudbase from "@cloudbase/js-sdk"
import adapter from "cloudbase-adapter-wx_mp";

...

    cloudbase.useAdapters(adapter);
    const app = cloudbase.init({
      env: "XXX",
      appSign: "XXX",
      appSecret: {
        appAccessKeyId: "1",
        appAccessKey: "XXX"
      }
    });    

    
    const auth = app.auth({ persistence: 'session' });          
    auth.anonymousAuthProvider().signIn().then(r=>{
      console.log(r)
      const db = app.database();
      db.collection('Attendees')
        .get()
        .then(res => {
          console.log(res)
        });
    }); 
```

Reference: https://developers.weixin.qq.com/community/minihome/doc/000466e59bcde86d60ff56a195b000

> **Problem** \
> Problem that the appAccessKey is not safe to store from front end of wechat mini app client side.
>
> 1. Create a mini api or 
> 2. use Cloud Function (HTTP request without permission) or 
> 3. Something like KeyValues

