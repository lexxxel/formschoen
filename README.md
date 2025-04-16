# build with

`west build -b nice_nano_v2 -S studio-rpc-usb-uart -- -DSHIELD=formschoen_left -DZMK_EXTRA_MODULES=../../formschoen/`
`west build -b nice_nano_v2 -S studio-rpc-usb-uart -- -DSHIELD=formschoen_right -DZMK_EXTRA_MODULES=../../formschoen/`

# flash

create `/etc/systemd/system/mnt-nicenano.mount`:

```systemd
[Unit]
Description=Mount Nice!Nano USB storage to /mnt/nicenano
After=dev-disk-by-label-NICENANO.device
Requires=dev-disk-by-label-NICENANO.device

[Mount]
What=/dev/disk/by-label/NICENANO
Where=/mnt/nicenano
Options=uid=1000,gid=1000,umask=000,nofail,x-systemd.device-timeout=3s
Type=vfat

[Install]
WantedBy=multi-user.target
```

and run once `mkdir -p /mnt/nicenano`.

Afterwards, flash with:
`sudo systemctl restart mnt-nicenano.mount && cp build/zephyr/zmk.uf2 /mnt/nicenano/`

# Helpful Layout Visualizer

`https://www.keyboard-layout-editor.com/##@_backcolor=%23ffffff&css=%3B&@_x:2&c=%23f5f5f5&t=%23000000%0A%0A%0A%2300d5f5%0A%0A%0A%23fc0d1b&sm=cherry&sb=gateron&st=KS-3-Red&fa@:0&:0&:0&:1%3B%3B&=E%0A%0A%0AToggle%20Output%0A%0A%0A%7B&_x:8&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c%3B&=I%0AF8%0A%0A%0A%0A%0A8%0A(%3B&@_y:-0.71&x:3&t=%23000000%0A%0A%0A%2300d5f5%0A%0A%0A%23fc0d1b%3B&=R%0A%0A%0APrev%20Profile%0A%0A%0A%7D&_x:6&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c%3B&=U%0AF7%0A%0A%0A%0A%0A7%0A%2F%2F%3B&@_y:-0.97&x:1&t=%23000000%0A%0A%0A%2300d5f5%3B&=W%0A%0A%0AStudio%20Unlock&_x:10&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c%3B&=O%0AF9%0A%0A%0A%0A%0A9%0A)%3B&@_y:-0.9000000000000001&x:9%3B&=Y%0AF12%0A%0A%0A%0A%0A+%0A*%3B&@_y:-0.9999999999999999&x:4&t=%23000000%0A%0A%0A%2300d5f5%3B&=T%0A%0A%0ANext%20Profile%3B&@_y:-0.47&t=%23000000%3B&=Q&_x:12&t=%23000000%0A%0A%0A%0A%0A%0A%2300ed2c%3B&=P%0A%0A%0A%0A%0A%0A%C3%9C%3B&@_y:-0.95&x:2&t=%23000000%0A%0A%0A%2300d5f5%0A%2300ed2c%0A%0A%23fc0d1b%3B&=D%0A%0A%0ABT1%0ANumbers%0A%0A(&_x:8&t=%23000000%0A%23e711f7%0A%0A%0A%23fc0d1b%0A%0A%2300ed2c%0A%2300ed2c%3B&=K%0AF5%0A%0A%0ABrackets%0A%0A5%0A%25%3B&@_y:-0.71&x:3&t=%23000000%0A%0A%0A%2300d5f5%0A%0A%0A%23fc0d1b%3B&=F%0A%0A%0ABT0%0AShift%0A%0A)&_x:6&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c%3B&=J%0AF4%0A%0A%0AShift%0A%0A4%0A$%3B&@_y:-0.97&x:1&t=%23000000%0A%0A%0A%2300d5f5%0A%23e711f7%0A%0A%23fc0d1b%3B&=S%0A%0A%0ABT2%0AF-Keys%0A%0A%3C%3B&@_y:-0.9999450000000003&x:12&t=%23000000%0A%23e711f7%0A%0A%0A%2300d5f5%0A%0A%2300ed2c%0A%2300ed2c%3B&=L%0AF6%0A%0A%0ABluetooth%0A%0A6%0A%2F&%3B&@_y:-0.9000549999999996&x:4&t=%23000000%0A%0A%0A%2300d5f5%0A%0A%0A%23fc0d1b%3B&=G%0A%0A%0ABT4%0A%0A%0A%3E&_x:4&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c%3B&=H%0AF11%0A%0A%0A%0A%0A%C3%9F%0A%3F%3B&@_y:-0.47&t=%23000000%0A%2300d5f5&f2:1%3B&=A%0ABT3&_x:12&t=%23000000%0A%0A%0A%0A%0A%0A%2300ed2c&f:3%3B&=%C3%96%0A%0A%0A%0A%0A%0A%C3%84%3B&@_y:-0.9500000000000002&x:2&t=%23000000%0A%0A%0A%2300d5f5%0A%0A%0A%23fc0d1b&f2:1%3B&=C%0A%0A%0ADis%20BT1%0A%0A%0A%5B&_x:8&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c&f:3%3B&=,%0AF2%0A%0A%0A%0A%0A2%0A%22%3B&@_y:-0.71&x:3&t=%23000000%0A%0A%0A%2300d5f5%0A%0A%0A%23fc0d1b&f2:1%3B&=V%0A%0A%0ADis%20BT0%0A%0A%0A%5D&_x:6&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c&f:3%3B&=M%0AF1%0A%0A%0A%0A%0A1%0A!%3B&@_y:-0.9699999999999998&x:1&t=%23000000%0A%0A%0A%2300d5f5%3B&=X%0A%0A%0ADis%20BT2&_x:10&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c&f:3%3B&=.%0AF3%0A%0A%0A%0A%0A3%0A%C2%A7%3B&@_y:-0.8999999999999999&x:4&t=%23000000%0A%0A%0A%2300d5f5%3B&=B%0A%0A%0ADis%20BT4&_x:4&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c&f:3%3B&=N%0AF10%0A%0A%0A%0A%0A0%0A%2F=%3B&@_y:-0.4700000000000002&x:13&t=%23000000%0A%0A%0A%23fea300%0A%23fea300%0A%0A%2300ed2c%0A%2300ed2c&f:3%3B&=-%0A%0A%0A%0AtoBase%0A%0A%23%0A'%3B&@_y:-0.9999450000000003&t=%23000000%0A%0A%0A%2300d5f5%3B&=Y%0A%0A%0ADis%20BT3%3B&@_y:1.0499450000000001&x:3&t=%23000000%3B&=UP&_x:6%3B&=UP%3B&@_x:2%3B&=LEFT&_t=%23000000%0A%0A%0A%0A%23fea300&a:7&f:2%3B&=%0A%0A%0A%0AGaming2&_t=%23000000&a:4&f:3%3B&=RIGHT&_x:4%3B&=LEFT&_a:7%3B&=&_a:4%3B&=RIGHT%3B&@_x:3%3B&=DOWN&_x:6%3B&=DOWN%3B&@_rx:3.5&ry:5&y:-1.4500000000000002&x:-0.5&t=%23000000%0A%0A%0A%0A%0A%0A%23fc0d1b%3B&=CTRL%0A%0A%0A%0A%0A%0A%7C%3B&@_rx:10.5&y:-1.4500000000000002&x:-0.5&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c&fa@:0&:1&:0&:0&:0&:0&:2%3B%3B&=BkSp%0APlay%2F%2FPause%0A%0A%0A%0A%0ADel%3B&@_r:15&rx:3.5&y:-1.6&x:0.3999999999999999&t=%23000000%0A%0A%0A%0A%2300d5f5%0A%0A%2300ed2c&fa@:0&:1&:0&:0&:1&:0&:2%3B%3B&=SPACE%0A%0A%0A%0AGaming%0A%0AALTG%3B&@_rx:10.5&y:-1.6&x:0.40000000000000036&t=%23000000%0A%23e711f7%0A%0A%2300d5f5%0A%0A%0A%2300ed2c%0A%2300ed2c&fa@:0&:1&:0&:1&:1&:0&:1&:1%3B%3B&=Tab%0A%3E%0A%0ABLClear%0A%0A%0A~%0A%C2%AF%3B&@_r:18&rx:3.5&y:-2.65&x:1.4000000000000004&t=%23000000%3B&=ESC%3B&@_r:-18&rx:10.5&y:-2.65&x:-2.4000000000000004&t=%23000000%0A%0A%0A%0A%0A%0A%2300ed2c%0A%2300ed2c&fa@:0&:1&:0&:1&:1&:0&:5&:5%3B%3B&=ALT%0A%0A%0A%0A%0A%0A%C2%B4%0A%60%3B&@_r:-15&rx:3.5&y:-1.6&x:-1.4&t=%23000000%0A%0A%0A%0A%0A%0A%23fc0d1b%0A%23fc0d1b&f:3%3B&=GUI%0A%0A%0A%0A%0A%0A%5E%0A%C2%B0%3B&@_rx:10.5&y:-1.6&x:-1.4000000000000004&t=%23000000%0A%23e711f7%0A%0A%0A%0A%0A%2300ed2c&fa@:0&:1&:0&:1&:1&:0&:2%3B%3B&=Enter%0A%3C%0A%0A%0A%0A%0ACaps`

Print via screenshot, the export tool is broken
