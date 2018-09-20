# MacOS - miner tutorial

## Install from Source

{% code-tabs %}
{% code-tabs-item title="\#install\_guide" %}
```bash
# Make sure you have homebrew installed (if you do, skip this step):
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# Make sure to install all required dependencies
brew install gmp make cmake openssl

# Get the latest source code (or run a git pull to update)
git clone https://github.com/OrdinaryDude/xel_miner

# Make sure to link the OpenSSL include directory to the right place
ln -s /usr/local/opt/openssl/include/openssl/ /usr/local/include/openssl

# Compile the miner
cd xel_miner
OPENSSL_ROOT_DIR=/usr/local/opt/openssl cmake .
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

{% embed data="{\"url\":\"https://vimeo.com/265864791\",\"type\":\"video\",\"title\":\"Install XEL miner from sources on macOS\",\"icon\":{\"type\":\"icon\",\"url\":\"https://i.vimeocdn.com/favicon/main-touch\_180\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"http://i.vimeocdn.com/video/695983158.jpg\",\"width\":2370,\"height\":1854,\"aspectRatio\":0.7822784810126582},\"embed\":{\"type\":\"player\",\"url\":\"https://player.vimeo.com/video/265864791?byline=0&badge=0&portrait=0&title=0\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 78.2595%;\\\"><iframe src=\\\"https://player.vimeo.com/video/265864791?byline=0&amp;badge=0&amp;portrait=0&amp;title=0\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.2778},\"caption\":\"xel\_miner on MacOS\"}" %}

{% page-ref page="linux.md" %}

>

