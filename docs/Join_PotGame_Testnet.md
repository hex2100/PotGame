#   A tutorial about Join PotGame Testnet for beginners

##  一台运行linux的电脑，比如ubuntu 18.0，debian(最好有一台服务器)

##  设置初始环境，包括安装一些依赖和 rust lang编程环境
```
curl https://getsubstrate.io -sSf | bash -s -- --fast
```

##  用subkey生成私钥文件
```
subkey generate --scheme sr25519
Secret phrase `trip pottery asthma canoe mom owner wagon student program drive sport float` is account:
  Secret seed:      0x047c9b1433700bdb5c6b0ac6ec0a805e70c94880e6f339d8e807662050a1f671
  Public key (hex): 0x247858589f463b1c3c474155cb8b5fac7adac195f84d5817134770fe893f575b
  Account ID:       0x247858589f463b1c3c474155cb8b5fac7adac195f84d5817134770fe893f575b
  SS58 Address:     5CtXL9eMxUzbvwfTMUACjpP5R9QreaFmMB1Vnkw2LibLh7xA
```

```
subkey generate --scheme ed25519
Secret phrase `broom renew aisle eagle paddle adjust shift income time system object width` is account:
  Secret seed:      0x1fa2f7bd373fb6ba618857b41c16bb656a3efd3b778c77f61be4b0bdd32a62c6
  Public key (hex): 0x655881d178a88874771ea7077a0addcb08b503d8d462444b8af411266eb5780f
  Account ID:       0x655881d178a88874771ea7077a0addcb08b503d8d462444b8af411266eb5780f
  SS58 Address:     5EMaz7sL1Z7LrL9Tka8YhFcwZsP1jXLQp4zdYNkTHettt9oV
```

用这个命令可以把密钥保存到文件
```
subkey generate --scheme ed25519 > key001.sr

```

##  运行节点
```
./target/release/node-template --chain stash --name "rococo" --base-path  /tmp/rococo --rpc-port 9934 --ws-port 9944 --port 30344 --validator --database parityDB
```

./target/release/node-template 这是你下载或编译的二进制程序的路径 

--name "rococo" 换成你喜欢的名字

--base-path     换成你喜欢的路径

##  导入私钥

### aura 对应 sr25519格式的私钥 
```
curl -X POST http://localhost:9933 -H "Content-Type:application/json;charset=utf-8" -d '{
    "jsonrpc":"2.0",
     "id":1, 
     "method":"author_insertKey", 
     "params": [
        "aura", 
        "trip pottery asthma canoe mom owner wagon student program drive sport float",
        "0x247858589f463b1c3c474155cb8b5fac7adac195f84d5817134770fe893f575b"
        ]
     }'
```

### gran 对应 ed25519格式的私钥

```
curl -X POST http://localhost:9933 -H "Content-Type:application/json;charset=utf-8" -d '{
    "jsonrpc":"2.0", 
    "id":1, 
    "method":"author_insertKey", 
    "params": [ 
        "gran", 
        "broom renew aisle eagle paddle adjust shift income time system object width",
        "0x655881d178a88874771ea7077a0addcb08b503d8d462444b8af411266eb5780f" 
        ]
    }'

```

### 重新启动节点
节点应该能正确运行了