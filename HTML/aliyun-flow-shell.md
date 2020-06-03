# 阿里云 云效构建Hugo脚本

默认使用goproxy.cn

export GOPROXY=https://goproxy.cn
# input your command here
git clone https://code.aliyun.com/eallion/gohugo.git
cd gohugo
dpkg -i hugo_0.70.0_Linux-64bit.deb
cd ..
rm -rf gohugo
hugo --cleanDestinationDir --forceSyncStatic --gc --ignoreCache --minify