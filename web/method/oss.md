# OSS前端上传

## 常见问题

- 图片类型文件格式错误，上传失败或者图片无效
  - [严格判断文件类型](https://www.cnblogs.com/SZPLove/p/15740503.html)
  - [利用文件头标识判断文件类型](https://www.cnblogs.com/senior-engineer/p/9541719.html)
  - [优化实战 第 17 期 - 文件类型的终极校验，堪称完美 - 掘金](https://juejin.cn/post/6999241171566329887)
  ![Untitled](/assets/web/技术/upload-1.png)

- 较大的视频上传失败
  - 调用PostObject接口的常见错误及解决方法
  - PostObject
  - 0006-00000213
  - 0006-00000003
    > 错误EC：0006-00000213，超时
    > 错误EC：0006-00000003，文件大小限制
    > 阿里云的工单：<https://smartservice.console.aliyun.com/service/robot-chat?id=0001Z9GSC6>
    > ![Untitled](/assets/web/技术/upload-2.png)

## 参考文档

- [服务端签名直传](https://help.aliyun.com/document_detail/31926.html?spm=a2c4g.31926.0.0)
- [aliy-oss SDK](https://github.com/ali-sdk/ali-oss)
- [PostObject](https://help.aliyun.com/zh/oss/developer-reference/postobject?spm=a2c4g.11186623.0.i31)
- [分片上传](https://help.aliyun.com/zh/oss/user-guide/multipart-upload-12?spm=a2c4g.11186623.0.0.caae58f8ys0bbW)
- [NodeJs分片上传](https://help.aliyun.com/document_detail/111268.html?spm=a2c4g.31992.0.0.3bdf2bbe7agKcL#concept-hgg-3vb-dhb)
- [Browser.js分片上传](https://help.aliyun.com/document_detail/383952.html?spm=5176.smartservice_service_robot_chat_new.0.0.1994f625LSKeFj#section-i82-h8t-p4g)
- [断点续传](https://help.aliyun.com/zh/oss/user-guide/resumable-upload?spm=a2c4g.11186623.0.0.3e1b78e8VeYtkm)
- [使用限制](https://help.aliyun.com/document_detail/54464.html?spm=a2c4g.64945.0.0.4a915656LOKcAb#concept-pzk-crg-tdb)
- [Demo1](https://www.cnblogs.com/flytree/p/16833447.html)
- [Demo2](https://blog.51cto.com/u_16175097/6588986)
- [严格判断文件类型](https://www.cnblogs.com/SZPLove/p/15740503.html)
- [利用文件头标识判断文件类型](https://www.cnblogs.com/senior-engineer/p/9541719.html)
- [调用PostObject接口的常见错误及解决方法](https://help.aliyun.com/zh/oss/how-to-handle-common-errors-when-the-postobject-operation-is-called?spm=a2c4g.11186623.0.0.566544fb5xsv4i)
- [OSS自动诊断工具](https://smartservice.console.aliyun.com/service/robot-chat?spm=5176.smartservice_service_create_ticket_step_1.0.0.13bb3f1bA674XL)
