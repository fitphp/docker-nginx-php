本项目为整合Nginx与PHP各版本Docker镜像与Compose。

## 主要特性
* 支持主流程PHP框架，如ThinkPHP5.0+、Laravel 8.0+
* 同时运行PHP多版本

## 开始使用
1：修改nginx-php.yml文件中的 `{WEBSITE_PATH}` 为项目路径，
也可使用`.env`环境变量文件定义，如：
```dotenv
# 站点目录地址
WEBSITE_PATH=/project/path
```

### 启动环境
```shell
# docker-compose -f nginx-php.yml up -d
```

### 参与开源
欢迎提交 [issue](https://gitee.com/fitphp/docker-nginx-php/issues)