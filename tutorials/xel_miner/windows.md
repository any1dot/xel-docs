# Windows - miner tutorial

## Install from binary

{% code-tabs %}
{% code-tabs-item title="\#install\_guide" %}
```bash
# Download the latest (experimental CPU only) binary version from:
https://github.com/xel-software/xel_miner_releases/files/1933994/xel_miner-0.9.6.zip
```
{% endcode-tabs-item %}
{% endcode-tabs %}

After you unzip the archive, go into the folder `xel_miner-0.9.6/xel_miner`. There, you will find the `xel_miner.exe` executable. You can test if it’s functioning properly by running:

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
xel_miner.exe --test-vm examples\SHA256_BTC.epl
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If you encounter any errors, the reason may be that you already have a MinGW installation on your system and in your `PATH`. In this case, try to clean the `PATH` variable by doing a simple

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
set PATH=
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Video tutorial

{% embed data="{\"url\":\"https://vimeo.com/265864726\",\"type\":\"video\",\"title\":\"Install XEL miner \(binary\) on Windows\",\"icon\":{\"type\":\"icon\",\"url\":\"https://i.vimeocdn.com/favicon/main-touch\_180\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"http://i.vimeocdn.com/video/695983095.jpg\",\"width\":3000,\"height\":1966,\"aspectRatio\":0.6553333333333333},\"embed\":{\"type\":\"player\",\"url\":\"https://player.vimeo.com/video/265864726?byline=0&badge=0&portrait=0&title=0\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 65.4536%;\\\"><iframe src=\\\"https://player.vimeo.com/video/265864726?byline=0&amp;badge=0&amp;portrait=0&amp;title=0\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.5278},\"caption\":\"xel\_miner on windows\"}" %}

{% page-ref page="macos.md" %}

>

