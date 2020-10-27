# Encrypt-Decrypt-App Assignment

## Exectue Unit test & Code coverage
```bash
python .\app-unittest.py                                               
.....
----------------------------------------------------------------------
Ran 5 tests in 0.007s

$ coverage run  .\app-unittest.py                                        
.........
----------------------------------------------------------------------
Ran 9 tests in 0.015s
OK

$ coverage report                                                        Name                                                                                   Stmts   Miss  Cover
----------------------------------------------------------------------------------------------------------
app-unittest.py                                                                           56      0   100%
app.py                                                                                    42      6    86%
----------------------------------------------------------------------------------------------------------
TOTAL                                                                                     98      6    93%
```

## Build container image and start docker container
```bash
# build docker image
$ docker build -t aksh245/encrpt-decrypt-app .

# check app docker image
$ docker images

# start app from docker image
$ docker run --name test-app -p 5000:5000 aksh245/encrpt-decrypt-app
```



## Rest calls
### Health Check /api/health
```bash
$ curl --header "Content-Type: application/json" \
  --request GET \
  http://localhost:5000/api/health
```
output
```
{
  "input": "",
  "message": "",
  "output": "ok",
  "status": "success"
}
```  
  
### Encrypt /api/encrypt

```bash
$ curl --header "Content-Type: application/json" \
  --request GET \
  --data '{"input": "My String to encrypt"}' \
  http://localhost:5000/api/encrypt
```
output:
```
{
  "input": "My String to encrypt",
  "message": "",
  "output": "TXkgU3RyaW5nIHRvIGVuY3J5cHQ=",
  "status": "success"
}
```
  
### Decrypt /api/decrypt
```bash  
$ curl --header "Content-Type: application/json" \
  --request GET \
  --data '{"input": "TXkgU3RyaW5nIHRvIGVuY3J5cHQ="}' \
  http://localhost:5000/api/decrypt
```
output
```
{
  "input": "TXkgU3RyaW5nIHRvIGVuY3J5cHQ=",
  "message": "",
  "output": "My String to encrypt",
  "status": "success"
}
```
## Helm Deployment
```bash
$ cd helm-deployment/encrypt-decrypt-app/
$ helm lint .
$ helm upgrade --install encrypt-decrypt-app .
```
