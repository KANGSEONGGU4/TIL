## flyctl

외부에서 fly.io 안쪽의 db에 바로접근이 불가능하기 때문에, 접근이 필요할 때 마다 flyctl proxy 명령어로 개구멍을 open해줘야 한다.

```
flyctl proxy 5432 -a [db]
```
