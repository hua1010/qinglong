## 功能

- 用于支持树莓派上部署docker和脚本，参考原作者whyour内容改编

## 部署

### 本机部署

1. 创建docker image

```bash
cd qinglong/docker-pi
sudo docker build -f Dockerfile -t whyour/qinglong:latest .
```

2. 启动容器

```bash
docker run -dit \
  -v $PWD/ql/data:/ql/data \
  -p 5700:5700 \
  --name qinglong \
  --hostname qinglong \
  --restart unless-stopped \
  whyour/qinglong:latest
```

3. 访问

打开你的浏览器，访问 http://{ip}:5700

## 使用

1. 内置命令

```bash
# 更新并重启青龙
ql update                                                    
# 运行自定义脚本extra.sh
ql extra                                                     
# 添加单个脚本文件
ql raw <file_url>                                             
# 添加单个仓库的指定脚本
ql repo <repo_url> <whitelist> <blacklist> <dependence> <branch> <extensions>
# 删除旧日志
ql rmlog <days>                                              
# 启动tg-bot
ql bot                                                       
# 检测青龙环境并修复
ql check                                                     
# 重置登录错误次数
ql resetlet                                                  
# 禁用两步登录
ql resettfa                                                  

# 依次执行，如果设置了随机延迟，将随机延迟一定秒数
task <file_path>                                             
# 依次执行，无论是否设置了随机延迟，均立即运行，前台会输出日，同时记录在日志文件中
task <file_path> now                                         
# 并发执行，无论是否设置了随机延迟，均立即运行，前台不产生日，直接记录在日志文件中，且可指定账号执行
task <file_path> conc <env_name> <account_number>(可选的) 
# 指定账号执行，无论是否设置了随机延迟，均立即运行 
task <file_path> desi <env_name> <account_number>         
```

2. 添加定时任务

依赖faker3 库
```bash
https://github.com/shufflewzc/faker3
并添加定时任务内容：
ql repo https://github.com/shufflewzc/faker3.git "jd_|jx_|gua_|jddj_|getJDCookie" "activity|backUp" "^jd[^_]|USER|function|utils|sendNotify|ZooFaker_Necklace.js|JDJRValidator_Pure|sign_graphics_validate|ql" "main"
```
需要注意的是这些都是第三方的脚本，且行且珍惜。感谢作者

