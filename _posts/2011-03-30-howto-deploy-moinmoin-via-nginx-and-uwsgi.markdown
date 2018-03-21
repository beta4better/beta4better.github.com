---
layout: post
title: Howto Deploy MoinMoin via Nginx and uWSGI
date: '2011-03-30 19:14:00'
---

<p>这里的内容不能保证是最新的，最新版在这里：<a href="http://wiki.beta4better.org/HowtoDeployMoinMoinviaNginxanduWSGI">via</a>，请移步。</p>

<p><strong>如何通过Nginx和uWSGI部署MoinMoin</strong></p>

<p>本<a href="http://www.beta4better.org/">Wiki</a>部署在<a href="http://enscloud.com/">eNetSouth Cloud</a>的VPS上，前端服务器为<a href="http://www.nginx.org/">Nginx</a>。大家可以从<a href="http://www.lowendbox.com/tag/enscloud-com/">这里</a>了解到<a href="http://enscloud.com/">eNetSouth Cloud</a>提供的VPS主机。</p>

<p>我会用这篇文章详细的介绍整个部署过程。如果有什么疑问可以到这里提问。</p>

<p>好了言归正传：</p>

<p>要进行下面的你需要对vps，nginx，python以及uwsgi有一些初步的了解，只要是稍微有一些基础知识就可以了，下面的过程基本上来说是很简单的，只要照着一步一步的做就可以了。</p>

<p><strong>服务器环境的配置</strong></p>

<p>VPS安装的系统是Debian Squeeze。首先用下面的命令安装必须的软件：</p>

<blockquote>
<p>apt-get update</p>
<p>apt-get upgrade</p>
<p>apt-get install build-essential libpcre3-dev libssl-dev psmisc python-dev libxml2 libxml2-dev python-setuptools</p>
</blockquote>

<p><strong>安装Nginx</strong></p>

<p>Nginx的安装暂不做详细介绍，我这里使用的版本是nginx/0.8.54。</p>

<p>为了后面能够通过域名访问wiki，需要在nginx下建立一个虚拟主机，配置文件可以通过<a href="http://c492911.r11.cf2.rackcdn.com/wiki.conf">这里</a>或者<a href="http://dl.dropbox.com/u/5807744/beta4better/uwsgi/wiki.conf">这里</a>下载到，放置到nginx配置文件夹下面就可以了。</p>

<blockquote>
<p>cd /etc/nginx/sites-enabled</p>
<p>wget <a href="http://c492911.r11.cf2.rackcdn.com/wiki.conf">http://c492911.r11.cf2.rackcdn.com/wiki.conf</a></p>
</blockquote>

<p>大家可能注意到uwsgi的启动脚本中有UWSGI_PYHOME、UWSGI_CHDIR和UWSGI_SCRIPT三个参数，分别指向 /usr/local/lib/python2.6/dist-packages、/usr/local/share/moin/server和moin.wsgi。这三个参数是运行moinmoin必需的，一定要写，后面会有详细的介绍。</p>

<p><strong>安装uWSGI</strong></p>

<p>可以从<a href="http://projects.unbit.it/uwsgi/wiki/WikiStart#Getit">这里</a>下载到uWSGI，有两个版本可以使用，<a href="http://projects.unbit.it/downloads/uwsgi-0.9.7.1.tar.gz">0.9.7.1</a>和<a href="http://projects.unbit.it/downloads/uwsgi-0.9.6.8.tar.gz">0.9.6.8</a>。0.9.7.1是current stable的版本，而0.9.6.8是long-term-support的版本，随便选一个就可以了。我这里使用的是0.9.7.1版本。详细的安装方法看<a href="http://projects.unbit.it/uwsgi/wiki/Install">这里</a>。简单的安装方法如下：</p>

<blockquote>
<p>cd /opt</p>
<p>tar zxf uwsgi-0.9.7.1.tar.gz</p>
<p>cd uwsgi-0.9.7.1</p>
<p>make -f Makefile.Py26</p>
</blockquote>

<p>安装完成后uwsgi位于/usr/bin/uwsgi中，将/usr/bin/uwsgi拷贝到/usr/local/bin中备用。这里之所以这么做是因为nginx我是用源码安装的，默认安装路径是在/usr/local/nginx中，拷贝过来的原因是为了方便管理。</p>

<p>从<a href="http://c492911.r11.cf2.rackcdn.com/moin-wsgi">这里</a>或者<a href="http://dl.dropbox.com/u/5807744/beta4better/uwsgi/moin-wsgi">这里</a>下载uwsgi的启动脚本，放置到/etc/init.d目录下：</p>

<blockquote>
<p>cd /etc/init.d/</p>
<p>wget <a href="http://c492911.r11.cf2.rackcdn.com/moin-wsgi">http://c492911.r11.cf2.rackcdn.com/moin-wsgi</a></p>
<p>chmod +x moin-uwsgi</p>
</blockquote>

<p>然后，通过下面的命令创建uwsgi的日志文件：</p>

<blockquote>
<p>touch /var/log/moin-uwsgi.log</p>
<p>chown www-data /var/log/moin-uwsgi.log</p>
</blockquote>

<p>最后，通过下面的命令启动uwsgi：</p>

<blockquote>
<p>/usr/sbin/update-rc.d -f moin-uwsgi defaults</p>
<p>/etc/init.d/moin-uwsgi start</p>
</blockquote>

<p>大家可能注意到uwsgi的启动脚本中有&#8212;pythonpath和&#8212;wsgi-file两个参数，分别指向 /usr/local/lib/python2.6/dist-packages 和/usr/local/share/moin/moin.wsgi。这两个目录是安装moinmoin时的位置，后面会有详细的介绍。</p>

<p>启动脚本中的参数，大家可以根据实际情况进行修改。</p>

<p><strong>安装MoinMoin</strong></p>

<p>这里我使用的MoinMoin的版本是1.9.3，大家可以从<a href="http://static.moinmo.in/files/moin-1.9.3.tar.gz">这里</a>下载到：</p>

<blockquote>
<p>cd /opt</p>
<p>wget <a href="http://static.moinmo.in/files/moin-1.9.3.tar.gz">http://static.moinmo.in/files/moin-1.9.3.tar.gz</a></p>
</blockquote>

<p>接下来进行解压并安装：</p>

<blockquote>
<p>tar zxf moin-1.9.3.tar.gz</p>
<p>cd moin-1.9.3</p>
<p>python2.6 setup.py install &#8212;force &#8212;prefix /usr/local &#8212;record=install.log</p>
<p>cd /usr/local/share/moin</p>
<p>cp server/moin.wsgi .</p>
<p>cp config/wikiconfig.py  .</p>
</blockquote>

<p>然后修改配置文件moin.wsgi，在a2）出增加下面一段：</p>

<blockquote>
<p>sys.path.insert(0, &#8216;/usr/local/share/moin&#8217;)</p>
</blockquote>

<p>接下来做一些必要的配置：</p>

<blockquote>
<p>cd /usr/local/share</p>
<p>chown -R www-data:www-data moin</p>
<p>chmod -R ug+rwX moin</p>
<p>chmod -R o-rwx moin</p>
</blockquote>

<p>到此便基本配置好了，修改一些必要的wiki配置信息就可以了。</p>

<blockquote>
<p>page_front_page = u&#8221;FrontPage&#8221;</p>
<p>superuser = [u&#8221;WikiAdmin&#8221;, ]</p>
</blockquote>

<p>至此，不出什么意外的话，MoinMoin就配置好了，通过wiki.conf里面的域名就可以访问了。</p>

<p>接下来，你需要去阅读下wiki的文档，做一些必要的配置，学一学wiki的语法就可以使用了。祝大家好运喽。</p>

<p>有什么问题，请大家到这里<a href="http://www.beta4better.org/questions/2/howto-deploy-moinmoin-via-nginx-and-uwsgi">留言</a>。</p>

<p>参考文档：</p>

<ul><li><a href="http://library.linode.com/web-servers/nginx/python-uwsgi/debian-6-squeeze">http://library.linode.com/web-servers/nginx/python-uwsgi/debian-6-squeeze</a></li>
<li><a href="http://wiki.osqa.net/display/docs/Home">http://wiki.osqa.net/display/docs/Home</a></li>
<li><a href="http://projects.unbit.it/uwsgi/wiki/Doc">http://projects.unbit.it/uwsgi/wiki/Doc</a></li>
<li><a href="http://projects.unbit.it/uwsgi/wiki/Example">http://projects.unbit.it/uwsgi/wiki/Example</a></li>
<li><a href="http://obmem.info/?p=703">http://obmem.info/?p=703</a></li>
<li><a href="http://blog.khsing.net/2010/10/run-moinmoin-under-uwsgi-and-n.html">http://blog.khsing.net/2010/10/run-moinmoin-under-uwsgi-and-n.html</a></li>
<li><a href="http://apt-blog.net/moinmoin-on-nginx-via-fastcgi-and-uwgi">http://apt-blog.net/moinmoin-on-nginx-via-fastcgi-and-uwgi</a></li>
<li><a href="http://farter.users.sourceforge.net/blog/2010/12/12/installing-osqa-with-nginx-uwsgi-and-sqlite3-on-ubuntu-lucid-10-04-minimal/">http://farter.users.sourceforge.net/blog/2010/12/12/installing-osqa-with-nginx-uwsgi-and-sqlite3-on-ubuntu-lucid-10-04-minimal/</a></li>
<li><a href="http://farter.users.sourceforge.net/blog/2011/02/11/running-osqa-with-nginx-and-uwsgi-virtualhosting-mode-with-dynamicapps/">http://farter.users.sourceforge.net/blog/2011/02/11/running-osqa-with-nginx-and-uwsgi-virtualhosting-mode-with-dynamicapps/</a></li>
</ul>