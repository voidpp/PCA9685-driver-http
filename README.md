About
-
This is a simple, thin web interface layer for accessing PCA9685 controller via for example Raspberry Pi.

For other details, see [PCA9685-driver](https://github.com/voidpp/PCA9685-driver).

Install
-
```bash
pip install PCA9685-driver-http
```
Do not use the ``run-dev-server.py`` in 'production', instead of this use [uWSGI](https://uwsgi-docs.readthedocs.org/en/latest/), or sg else.

Example config for uwsgi: (`/etc/uwsgi/apps-enabled/PCA9685-driver-http.ini`)

```ini
[uwsgi]
processes = 2
module = pca9685_driver_http.app:app
http-socket = :52042
```
The default user of the uwsgi process is `www-data`, so need to add the `www-data` user to the `i2c` group.

For example: `usermod -G i2c -a www-data`

API endpoints test examples with `curl`
-
```bash
curl http://localhost:52042/devices/lamp/led/7
# {"result": "ok", "value": 10}
curl http://localhost:52042/devices/lamp/led/7 -X PUT -d value=10 
# {"result": "ok"}
curl http://localhost:52042/devices/lamp/led
# {"result": "ok", "values": {"0": 4096, "1": 4096, "2": 4096, "3": 0, "4": 4096, "5": 0, "6": 0, "7": 10, "8": 4196, "9": 4096, "10": 4096, "11": 4096, "12": 4096, "13": 4096, "14": 4096, "15": 4096}}
curl http://localhost:52042/devices/lamp/led -X PUT -d "led[5]=10&led[6]=10"
# {"result": "ok"}
curl http://localhost:52042/devices/lamp/pwm-frequency
# {"result": "ok", "value": 1017}
curl http://localhost:52042/devices/lamp/pwm-frequency -X PUT -d value=1017
# {"result": "ok"}
curl http://localhost:52042/devices/lamp/led/42
# {"result": "error", "message": "led_number must be less than 15, got 42"}
```
