



## 全局安装 newman
```shell
pnpm add -g newman
```
## 全局安装  newman-reporter-htmlextra
```shell
pnpm add -g newman-reporter-htmlextra
```
##  pnpm list
```shell
pnpm list -g --depth=0
Legend: production dependency, optional only, dev only
/Users/he/Library/pnpm/global/5
dependencies:
newman 6.2.1
newman-reporter-htmlextra 1.23.1
```
## 运行
```shell
newman run Ction.postman_collection.json -e dev.postman_environment.json -r htmlextra,cli
```