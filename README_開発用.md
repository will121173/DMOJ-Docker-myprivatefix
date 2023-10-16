# DMOJ Docker

Related
- [site](https://github.com/goropikari/online-judge)
- [judge server](https://github.com/goropikari/judge-server)

## Setup

```bash
# start web server and judge server
git clone https://github.com/goropikari/dmoj_docker.git
cd dmoj_docker
docker compose up -d

# stop system
docker compose down
```

Access http://127.0.0.1:8080/admin
- user name: admin
- password: admin


## For me
### Push images
Build site and judger docker images.

push image to dockerhub
```
make push-image

# push only site image
make push-site-image
```

### Development

```
make dev-build
make dev-run
```

```cpp
#include<iostream>
using namespace std;
int main() {
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) {
        int a, b;
        cin >> a >> b;
        cout << a+b << endl;
    }
}
```

```python
n = int(input())
for i in range(n):
    a, b = map(int, input().split())
    print(a+b)
```


# ここから追記

## make用意

https://www.docker.com/products/docker-desktop/

https://gnuwin32.sourceforge.net/packages/make.htm

```
$new_dir = "C:\Program Files (x86)\GnuWin32\bin"
$new_path = [Environment]::GetEnvironmentVariable("Path", "User")
$new_path += ";$new_dir"
[Environment]::SetEnvironmentVariable("Path", $new_path, "User")
```

## イメージ保存と読み込み
```
docker save dmoj-site -o dmoj-site.tar
docker load -i dmoj-site.tar
docker load -i dmoj-site-modified.tar
```

```
docker tag goropikari/dmoj-site myprivatefix/dmoj-site
```

## 編集手順

編集はじめだけ1回　コンテナ実行中に名前変える
```
docker tag goropikari/dmoj-site myprivatefix/dmoj-site
```

その後
```
docker compose up -d
docker ps -a
docker exec -it web /bin/bash
docker commit web myprivatefix/dmoj-site:latest
docker commit web goropikari/dmoj-site:latest
docker compose down
docker save goropikari/dmoj-site -o dmoj-site-modified.tar
docker save myprivatefix/dmoj-site -o dmoj-site.tar
```
vscodeなどで編集しても良い

http://127.0.0.1:8080/admin


```
docker cp readme.md web:/etc/test.txt
```

