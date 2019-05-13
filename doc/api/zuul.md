http://localhost:9300/merchant/merchant/getById?id=1

http://localhost:9300/mall/merchant/getById?id=1
```
curl -v -G 'http://localhost:9300/merchant/merchant/getById' \
  --data-urlencode 'id=1'

curl -v -G 'http://localhost:9300/mall/merchant/getById' \
  --data-urlencode 'id=1'
```
