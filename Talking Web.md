## lvl-6


```
>>> import requests
>>> head = {"host":"02e906fcac06457f6015ef2fc9af5d5e"}
>>> r = requests.get("http://127.0.0.1:80",headers=head)
>>> print(r.text)
```
pwn.college{practice}



## lvl-7


```
curl  http://localhost/9d209c2d1d604e4035acb15b05b2428a
```

pwn.college{practice}



## lvl-8


```
printf “GET / HTTP/1.0\r\n\r\n” | nc localhost 80
/2c293ea05569c2507d59340328edd27d

echo -e "GET http://127.0.0.1/2c293ea05569c2507d59340328edd27d HTTP/1.1\r\nHost: 127.0.0.1\r\n\r\n" | nc 127.0.0.1 80
```

pwn.college{practice}



## lvl-9


```
r = requests.get("http://127.0.0.1:80/4187d576a3289bae97ce2720905cadf7")
`/4187d576a3289bae97ce2720905cadf7`
```

pwn.college{practice}



## lvl-10


```
curl -G -v "http://localhost:80/data" --data-urlencode "msg=hello world" --data-urlencode "msg2=hello world2"
Incorrect path: value `/data`, should be `/ad1694e2 323f9d7a/098ed407 bd047151`

curl --get -v \
--data-urlencode 'product=$@mething useful' \
--data-urlencode 'quantity=22.5' \
--data-urlencode 'price=$55' \
https://example.org

curl --get -v --data-urlencode '/ad1694e2 323f9d7a/098ed407 bd047151' http://127.0.0.1:80

curl 'http://example.com/path/to/resource/path with spaces/and/special&characters' \
--path-as-is

curl 'http://127.0.0.1:80/%2Fad1694e2%20323f9d7a%2F098ed407%20bd047151'
```

pwn.college{practice}


## lvl-11


```
printf 'GET / HTTP/1.0\r\nHost:127.0.0.1:80\r\n\r\n' | nc 127.0.0.1 80
HTTP/1.1 400 BAD REQUEST
Server: Werkzeug/2.2.3 Python/3.8.10
Date: Fri, 31 Mar 2023 06:08:32 GMT
Content-Length: 76
Server: pwn.college
Connection: close

Incorrect path: value `/`, should be `/9db2bcdc 45f95e6c/5f84161b 7aba839e`

echo -e 'GET %2F9db2bcdc%2045f95e6c%2F5f84161b%207aba839e HTTP/1.0\r\nHost:127.0.0.1:80\r\n\r\n' | nc 127.0.0.1 80
HTTP/1.1 200 OK
Server: Werkzeug/2.2.3 Python/3.8.10
Date: Fri, 31 Mar 2023 06:13:07 GMT
Content-Length: 57
Server: pwn.college
Connection: close
```

pwn.college{practice}



## lvl-12


```
>>> import requests
>>> import urllib.parse
>>> path = '/50958459 1768d615/e82d7e5e 141ec0f4'
>>> encoded_path = urllib.parse.quote(path)
>>> print(encoded_path)
/50958459%201768d615/e82d7e5e%20141ec0f4
>>> r = requests.get('http://127.0.0.1:80/50958459%201768d615/e82d7e5e%20141ec0f4')
>>> print(r.text)
```

pwn.college{practice}



## lvl-13


```
curl -X GET "http://localhost:5000/locations?id=3"

4bb6e543bca66037e4b0738f88d890eb


url -D- -X POST --data '{"fields":{"project":{"key": "CCM"},"summary": "$1 at $2" ,"description": "$3","issuetype": {"name": "Service Request"}}}'

curl -D "a:4bb6e543bca66037e4b0738f88d890eb" http://127.0.0.1:80

curl -X POST -d 'a=4bb6e543bca66037e4b0738f88d890eb' http://127.0.0.1:80

looks like /?a=hashvalue

curl http://127.0.0.1:80/?a=f57d9928500657694b7e1d747f1254f3
```

pwn.college{practice}


## lvl-14


```
echo -e "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n" | nc example.com 80

Incorrect arg `a`: value `None`, should be `c09353fd7716b4952faa34cbd04cb9d3`

echo -e " GET /?a=c09353fd7716b4952faa34cbd04cb9d3 HTTP/1.0\r\nHost:127.0.0.1\r\n\r\n" | nc 127.0.0.1 80

HTTP/1.1 200 OK
Server: Werkzeug/2.2.3 Python/3.8.10
Date: Sun, 02 Apr 2023 02:58:51 GMT
Content-Length: 57
Server: pwn.college
Connection: close
```

pwn.college{practice}


## lvl-15


```
>>> import requests
>>> r = requests.get("http://127.0.0.1:80/a?=")
>>> print(r.text)
Incorrect arg `a`: value `None`, should be `bbdf3bcd595786a215966309616337ba`

>>> r = requests.get("http://127.0.0.1:80/a?=bbdf3bcd595786a215966309616337ba")
>>> print(r.text)
Incorrect arg `a`: value `None`, should be `bbdf3bcd595786a215966309616337ba`

>>> r = requests.get("http://127.0.0.1:80/?a=bbdf3bcd595786a215966309616337ba")
>>> print(r.text)
```

pwn.college{practice}



## lvl-16


```
hacker@talking-web-level-16:/run/challenge$ curl http://127.0.0.1:80/?a=
Incorrect arg `a`: value ``, should be `a7f7358b251b7474f48e69b8f3532467`
hacker@talking-web-level-16:/run/challenge$ curl http://127.0.0.1:80/?a=a7f7358b251b7474f48e69b8f3532467
Incorrect arg `b`: value `None`, should be `4fc781ad 8a9c2d5d&6bac5bc4#9cea7c87`
hacker@talking-web-level-16:/run/challenge$ curl http://127.0.0.1:80/?a=a7f7358b251b7474f48e69b8f3532467&b=4fc781ad%208a9c2d5d&6bac5bc4#9cea7c87
[1] 1274
[2] 1275
bash: 6bac5bc4#9cea7c87: command not found
[2]+  Done                    b=4fc781ad%208a9c2d5d
hacker@talking-web-level-16:/run/challenge$ Incorrect arg `b`: value `None`, should be `4fc781ad 8a9c2d5d&6bac5bc4#9cea7c87`
^C
[1]+  Done                    curl http://127.0.0.1:80/?a=a7f7358b251b7474f48e69b8f3532467
hacker@talking-web-level-16:/run/challenge$ curl http://127.0.0.1:80/?a=a7f7358b251b7474f48e69b8f3532467&b=4fc781ad%208a9c2d5d%266bac5bc4%239cea7c87


curl 'http://127.0.0.1:80/?a=a7f7358b251b7474f48e69b8f3532467&b=4fc781ad%208a9c2d5d%266bac5bc4%239cea7c87'
(after url encoding b)
```

pwn.college{practice}



## lvl-17


```
echo -e "GET / HTTP/1.0\r\nHost:127.0.0.1\r\n\r\n" | nc 127.0.0.1 80

Incorrect arg `a`: value `None`, should be `2997e564dbca298f5f1282e278af1b00`

hacker@talking-web-level-17:/run/challenge$ echo -e "GET /?a=2997e564dbca298f5f1282e278af1b00 HTTP/1.0\r\nHost:127.0.0.1\r\n\r\n" | nc 127.0.0.1 80

HTTP/1.1 400 BAD REQUEST
Server: Werkzeug/2.2.3 Python/3.8.10
Date: Sun, 02 Apr 2023 03:15:43 GMT
Content-Length: 81
Server: pwn.college
Connection: close

Incorrect arg `b`: value `None`, should be `738ba79d fd0c387b&e80a275e#a619ee44`
hacker@talking-web-level-17:/run/challenge$ echo -e "GET /?a=2997e564dbca298f5f1282e278af1b00&b=738ba79d%20fd0c387b%26e80a275e%23a619ee44 HTTP/1.0\r\nHost:127.0.0.1\r\n\r\n" | nc 127.0.0.1 80
HTTP/1.1 200 OK
Server: Werkzeug/2.2.3 Python/3.8.10
Date: Sun, 02 Apr 2023 03:16:21 GMT
Content-Length: 57
Server: pwn.college
Connection: close
```

pwn.college{practice}
(after url encoding the argument b)



## lvl-18


```
>>> import requests
>>> r = requests.get("http://127.0.0.1:80/?a=")
>>> print(r.text)
Incorrect arg `a`: value ``, should be `d5dcf8b4710c00ec6b2cd533ffb03d48`

>>> r = requests.get("http://127.0.0.1:80/?a=d5dcf8b4710c00ec6b2cd533ffb03d48")
>>> print(r.text)
Incorrect arg `b`: value `None`, should be `cf7d9868 7c399ff8&c3d9109f#43def444`

>>> r = requests.get("http://127.0.0.1:80/?a=d5dcf8b4710c00ec6b2cd533ffb03d48&b=cf7d9868%207c399ff8%26c3d9109f%2343def444")
>>> print(r.text)
```

pwn.college{practice}



## lvl-19


```
hacker@talking-web-level-19:/run/challenge$ curl -d "" http://127.0.0.1:80
Incorrect form `a`: value `None`, should be `b9a7032075b2dbd2bcbbd41b055a7aff`
hacker@talking-web-level-19:/run/challenge$ curl -d "a=b9a7032075b2dbd2bcbbd41b055a7aff" http://127.0.0.1:80
```

pwn.college{practice}



## lvl-20


```
echo -e "GET / HTTP/1.0\r\nHost:127.0.0.1\r\n\r\n" | nc 127.0.0.1 80

Incorrect form `a`: value `None`, should be `9043779ba85f27bae756e832ce90b8df`

echo -ne "POST /?a=9043779ba85f27bae756e832ce90b8df HTTP/1.1\r\nHost: 127.0.0.1\r\n\r\n" | nc 127.0.0.1 80

echo -e "GET /?a=9043779ba85f27bae756e832ce90b8df HTTP/1.0\r\nHost:127.0.0.1\r\n\r\n" | nc 127.0.0.1 80

echo -ne "GET /?a=9043779ba85f27bae756e832ce90b8df HTTP/1.1\r\nHost: 127.0.0.1\r\n\r\n" | nc 127.0.0.1 80

echo -ne "POST / HTTP/1.1\r\nHost: 127.0.0.1\r\nContent-Type: application/x-www-form-urlencoded\r\nContent-Length: 100\r\n\r\na=9043779ba85f27bae756e832ce90b8df" | nc 127.0.0.1 80

echo -e "POST / HTTP/1.1\nContent-Type: application/x-www-form-urlencoded\nContent-Length:34\n\na=9043779ba85f27bae756e832ce90b8df\r\n" | nc localhost 80

echo -e "POST / HTTP/1.1\nContent-Type: application/x-www-form-urlencoded\nContent-Length:34\n\na=9043779ba85f27bae756e832ce90b8df\r\n" | nc localhost 80
HTTP/1.1 200 OK
Server: Werkzeug/2.2.3 Python/3.8.10
Date: Sun, 02 Apr 2023 10:00:58 GMT
Content-Length: 57
Server: pwn.college
Connection: close
```

pwn.college{practice}
echo -n "a=9043779ba85f27bae756e832ce90b8df" | wc -c --> to get content length



## lvl-21


```
>>> import requests
>>> url = '127.0.0.1:80'
>>> data = {'a':'26f3c3336f83348f9d74431c2b5a2876'}
>>> r = requests.post(url, data=data)

>>> import requests
>>> url = 'http://127.0.0.1:80'
>>> data = {'a': '26f3c3336f83348f9d74431c2b5a2876'}
>>> response = requests.post(url, data=data)
>>> print(response.text)
```
pwn.college{practice}



## lvl-22


```
hacker@talking-web-level-22:/run/challenge$ curl -d "" http://127.0.0.1:80
Incorrect form `a`: value `None`, should be `bdf0aeb38a73c35c7599f7a6f066cf4e`
hacker@talking-web-level-22:/run/challenge$ curl -d "a=bdf0aeb38a73c35c7599f7a6f066cf4e" http://127.0.0.1:80
Incorrect form `b`: value `None`, should be `2a6a6cd5 3d99c210&fd384838#66be8337`
hacker@talking-web-level-22:/run/challenge$ curl -d "a=bdf0aeb38a73c35c7599f7a6f066cf4e&b=2a6a6cd5%203d99c210%26fd384838%2366be8337" http://127.0.0.1:80
```

pwn.college{practice}



## lvl-23


```
echo -e "POST / HTTP/1.1\nContent-Type: application/x-www-form-urlencoded\nContent-Length:78\n\na=ab40fc3ba2c603ac13c3f1b0d5c747c0&b=e2dcee77%202aa16da0%26a728c5f3%23387cb732\r\n" | nc localhost 80

Incorrect form `a`: value `9043779ba85f27bae756e832ce90b8df`, should be `ab40fc3ba2c603ac13c3f1b0d5c747c0`

Incorrect form `b`: value `None`, should be `e2dcee77 2aa16da0&a728c5f3#387cb732`

echo -e "POST / HTTP/1.1\nContent-Type: application/x-www-form-urlencoded\nContent-Length:45\n\na=ab40fc3ba2c603ac13c3f1b0d5c747c0&b=e2dcee77%202aa16da0%26a728c5f3%23387cb732" | nc 127.0.0.1 80

printf 'POST / HTTP/1.1\r\nHost: localhost\r\nContent-Type: application/x-www-form-urlencoded\r\nContent-Length: 79\r\n\r\na=ab40fc3ba2c603ac13c3f1b0d5c747c0&b=e2dcee77%202aa16da0%26a728c5f3%23387cb732' | nc localhost 80

echo -e "POST / HTTP/1.1\r\nContent-Type: application/x-www-form-urlencoded\r\nContent-Length: 79\r\n\r\na=ab40fc3ba2c603ac13c3f1b0d5c747c0&b=e2dcee77%202aa16da0%26a728c5f3%23387cb732\r\n" | nc 127.0.0.1 80

a=ab40fc3ba2c603ac13c3f1b0d5c747c0&b=e2dcee77%202aa16da0%26a728c5f3%23387cb732


echo -e "POST / HTTP/1.1\nContent-Type: application/x-www-form-urlencoded\nContent-Length:78\n\na=ab40fc3ba2c603ac13c3f1b0d5c747c0&b=e2dcee77%202aa16da0%26a728c5f3%23387cb732\r\n" | nc localhost 80
```

>Somtime content lenght is annoying. 
>https://www.browserling.com/tools/text-length

pwn.college{practice}



## lvl-24


```
>>> import requests
>>> url = 'http://127.0.0.1:80'
>>> data = {'a': '39b788a21d02c0bfd9251c0421d5a59a', 'b': 'fa919d3e 0d151266&b703d6a9#6d8fb72f'}
>>> r = requests.post(url, data=data)
>>> print(r.text)

>>> import requests
>>> url = 'http://127.0.0.1:80'
>>> data = {'a': '39b788a21d02c0bfd9251c0421d5a59a'}
>>> r = requests.post(url, data=data)
>>> print(r.text)

Incorrect form `b`: value `None`, should be `fa919d3e 0d151266&b703d6a9#6d8fb72f`

>>> data = {'a': '39b788a21d02c0bfd9251c0421d5a59a', 'b': 'fa919d3e 0d151266&b703d6a9#6d8fb72f'}


>>> import requests
>>> url = 'http://127.0.0.1:80'
>>> data = {'a': '39b788a21d02c0bfd9251c0421d5a59a', 'b': 'fa919d3e 0d151266&b703d6a9#6d8fb72f'}
>>> r = requests.post(url,data=data)
>>> print(r.text)
```

pwn.college{practice}


## lvl-25


```
curl -X POST -H "Content-Type: application/json" -d '{"key": "value"}' http://127.0.0.1:80

hacker@talking-web-level-25:/run/challenge$ curl -X POST -H "Content-Type: application/json" -d '{"key": "value"}' http://127.0.0.1:80
Incorrect json `a`: value `None`, should be `55bcbf883c60a2c8db88bc097c09d302`
hacker@talking-web-level-25:/run/challenge$ curl -X POST -H "Content-Type: application/json" -d '{"a": "55bcbf883c60a2c8db88bc097c09d302"}' http://127.0.0.1:80
```

pwn.college{practice}


## lvl-26


```
echo -e "POST / HTTP/1.1\nContent-Type: application/json\nContent-Length:78\n\na=ab40fc3ba2c603ac13c3f1b0d5c747c0&b=e2dcee77%202aa16da0%26a728c5f3%23387cb732\r\n" | nc localhost 80

echo -e "POST / HTTP/1.1\nContent-Type: application/json\r\nContent-Length: 34\r\na=ab40fc3ba2c603ac13c3f1b0d5c747c0" | nc localhost 80

hacker@talking-web-level-26:/run/challenge$ nc localhost 80
POST / HTTP/1.1
Host: 127.0.0.1
Content-Type: application/json
Content-Length: 40

{"a":"86d15008f64aed66a325a297e89fc982"}
HTTP/1.1 200 OK
Server: Werkzeug/2.2.3 Python/3.8.10
Date: Mon, 03 Apr 2023 19:56:52 GMT
Content-Length: 57
Server: pwn.college
Connection: close
```

pwn.college{practice}



## lvl-27


```
>>> import requests
>>> import json
>>> url = "http://127.0.0.1:80"
>>> data = {"a": "c4944e2b7b84c79eca17d4582b435667"}
>>> headers = {"Content-Type": "application/json"}
>>> response = requests.post(url, data=json.dumps(data), headers=headers)
>>> print(response.content)
b'pwn.college{practice}\n'
>>> print(response.text)
```

pwn.college{practice}

>response = requests.post(url, data=data, headers=headers) #shows error
