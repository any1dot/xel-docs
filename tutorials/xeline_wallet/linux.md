# Linux - xeline tutorial

## Install from binary

{% code-tabs %}
{% code-tabs-item title="\#install\_guide" %}
```bash
# Make sure unzip is installed
sudo apt-get install -y unzip

# Download the latest linux zip archive from:
https://github.com/xel-software/xeline/releases/latest

# Unzip the downloaded zip archive
unzip xeline-linux.zip

# Go into the directory containing the binary and launch it
cd Xeline-linux-x64
./Xeline
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## **Install from source:**

{% code-tabs %}
{% code-tabs-item title="\#install\_guide" %}
```bash
# Make sure curl and git are installed
sudo apt-get install -y curl git

# Install a recent version of nodejs first, if you haven't already.
#For Ubuntu/Debian is works like this
curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
sudo apt-get install -y nodejs

# Get the repository
git clone https://github.com/xel-software/xeline.git

# Or if you already have it, cd into the directory containing your xeline sources and update the code
cd xeline
git pull

# Now, go into the directory containing your xeline sources and install all dependencies
# (needs to be done only once)
cd xeline
npm install

# And finally, run the application
npm start
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Video tutorial

{% embed data="{\"url\":\"https://vimeo.com/265864522\",\"type\":\"video\",\"title\":\"Install Xeline wallet \(binary\) on Linux\",\"icon\":{\"type\":\"icon\",\"url\":\"https://i.vimeocdn.com/favicon/main-touch\_180\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"http://i.vimeocdn.com/video/695982855.jpg\",\"width\":3262,\"height\":2072,\"aspectRatio\":0.6351931330472103},\"embed\":{\"type\":\"player\",\"url\":\"https://player.vimeo.com/video/265864522?byline=0&badge=0&portrait=0&title=0\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 63.3794%;\\\"><iframe src=\\\"https://player.vimeo.com/video/265864522?byline=0&amp;badge=0&amp;portrait=0&amp;title=0\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.5778},\"caption\":\"linux video tutorial\"}" %}

{% page-ref page="../xel\_miner/" %}

>

