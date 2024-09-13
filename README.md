



## 全局安装 newman
pnpm add -g newman
## 全局安装 
pnpm add -g newman-reporter-htmlextra-extended
## 运行
newman run Ction.postman_collection.json -e dev.postman_environment.json -r htmlextra-extended,cli