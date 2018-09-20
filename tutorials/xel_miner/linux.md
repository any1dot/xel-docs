# Linux - miner tutorial

## Install from Source

{% code-tabs %}
{% code-tabs-item title="\#install\_guide" %}
```bash
# Make sure you have all dependencies installed
sudo apt-get install git libgmp-dev libcurl4-openssl-dev libssl-dev build-essential cmake

# Get the latest source code (or run a git pull to update)
git clone https://github.com/OrdinaryDude/xel_miner

# Run CMake inside xel_miner folder
cd xel_miner
cmake .

# Compile
make
```
{% endcode-tabs-item %}
{% endcode-tabs %}

You can test if it’s functioning properly by running:

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
xel_miner --test-vm examples/SHA256_BTC.epl
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Video tutorial

{% embed data="{\"url\":\"https://vimeo.com/265864834\",\"type\":\"video\",\"title\":\"Install XEL miner from sources on Linux\",\"icon\":{\"type\":\"icon\",\"url\":\"https://i.vimeocdn.com/favicon/main-touch\_180\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"http://i.vimeocdn.com/video/695983177.jpg\",\"width\":2814,\"height\":1724,\"aspectRatio\":0.6126510305614783},\"embed\":{\"type\":\"player\",\"url\":\"https://player.vimeo.com/video/265864834?byline=0&badge=0&portrait=0&title=0\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 61.2257%;\\\"><iframe src=\\\"https://player.vimeo.com/video/265864834?byline=0&amp;badge=0&amp;portrait=0&amp;title=0\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.6333},\"caption\":\"xel\_miner on linux\"}" %}

{% page-ref page="how\_to\_use.md" %}

>

