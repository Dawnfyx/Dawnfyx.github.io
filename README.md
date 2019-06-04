# jekyll + github pages = myblog

### run
jekyll serve --watch


### gem 修改镜像源

#### 要注意的是，ruby版本最好在2.0以上

#### 1.修改gem源
    
    //查看源：
    gem sources -l 
    //图内镜像：
    gem sources -a https://gems.ruby-china.com/
    //删除源：
    gem sources -r https://rubygems.org/ 
    
    
    //提示证书验证失败：
    C:\>gem sources -a https://gems.ruby-china.com/
    Error fetching https://gems.ruby-china.org/:
            SSL_connect returned=1 errno=0 state=SSLv3 read server
    rtificate verify failed (https://gems.ruby-china.org/specs.4.8.gz)
    
    
    //解决：下载证书：
    http://curl.haxx.se/ca/cacert.pem
    设置环境变量：
    SSL_CERT_FILE=<证书存放路径>
    如：SSL_CERT_FILE=d:\RailsInstaller\cacert.pem
    重启命令行，再次执行命令
    
    //如果还有问题，在命令行里执行
    set SSL_CERT_FILE=<证书存放路径>
    
    
#### 2.修改rails默认源
    bundle config 'mirror.https://rubygems.org' 'https://gems.ruby-china.com/'
