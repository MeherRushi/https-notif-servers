
# Fast API Implemtation

- Fast API is based on ASGI based implemenation - based on uvicorn


- Here, we enable SSL using certificates  and they are generated using the following command

```bash
openssl req -x509 -newkey rsa:2048 -keyout keyfile.pem -out certfile.pem -days 365 -nodes
```

- command to run 

```bash
uvicorn main:app --host 127.0.0.1 --port 8080 --ssl-keyfile ../../certs/server.key --ssl-certfile ../../certs/server.crt

```

gunicorn deployment:
```bash
gunicorn -w 5 -k uvicorn.workers.UvicornWorker --certfile=../../certs/server.crt --keyfile=../../certs/server.key -b 127.0.0.1:4433 main:app
```


Eg for valid json data

```
{
    "ietf-https-notif:notification": {
    "eventTime": "2013-12-21T00:01:00Z",
    "event" : {
        "event-class" : "fault",
        "reporting-entity" : { "card" : "Ethernet0" },
        "severity" : "major"
    }
    }
}
```

Eg for valid xml data

```
<notification xmlns="urn:ietf:params:xml:ns:netconf:notification:1.0">
  <eventTime>2013-12-21T00:01:00Z</eventTime>
  <event>
    <event-class>fault</event-class>
    <reporting-entity>
      <card>Ethernet0</card>
    </reporting-entity>
    <severity>major</severity>
  </event>
</notification>
```


