ALSA Hook
=========

A simple ALSA hook is used to publish MQTT messages when a hooked ALSA PCM is opened or closed.
It works with the ALSA `hooks` plugin.

## Install
```
sudo apt install libasound2-dev
make
sudo make install
```

## Configure
add the hooked pcm to `/etc/asound.conf` or `~/.asoundrc`

```
# hook entry
pcm_hook_type.voicen {
    install "_snd_pcm_hook_voicen_install"
    lib "alsa_hook_voicen.so"
}

pcm.hooked {
    type hooks
    slave.pcm "hw:0"

    hooks.0 {
        type "voicen"
    }
}
```

## MQTT messages
1.  when a hooked pcm is opened

    + topic: `/voicen/pcm/open` 
    + message: {pid}

2.  when a hooked pcm is closed

    + topic: `/voicen/pcm/close` 
    + message: {pid}
