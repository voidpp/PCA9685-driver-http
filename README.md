# About
This is a simple, thin web interface layer for accessing PCA9685 controller via for example Raspberry Pi.

For other details, see [PCA9685-driver](https://github.com/voidpp/PCA9685-driver).

# Install
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
