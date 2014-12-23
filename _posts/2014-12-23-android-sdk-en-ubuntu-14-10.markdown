---
layout: post
title:  "Android SDK en Ubuntu 14.10"
date:   2014-12-23 06:39:14
categories: how-to
tags: [Android, Ubuntu]
---

Por asunto de trabajo por estos dias estoy retomando mis practicas de programación para a plataforma [Android][android], si estas usando [Ubuntu][ubuntu] 14.10 x64 al igual que yo, aún luego de seguir la documentación oficial de Android para developers tendrás un problema al momento de correr tu aplicación.

Lo que sucede es que la [SDK][sdk] necesita las librerias de 32bits, leyendo algunos webs recomiendan instalar el paquete ia32-libs el cual no se encuentra en Ubuntu 14.10.

Luego de varios tropiezos me tope con este [articulo][articulo], el problema se resuelve en dos pasos:

# Android Debug Bridge (adb)

#### Error:

{% highlight bash %}
...error while loading shared libraries: libstdc++.so.6: cannot open shared object file: No such file or directory
{% endhighlight %}

#### Solución:

{% highlight bash %}
$ sudo aptitude install lib32stdc++6
{% endhighlight %}

#### Comprobamos que ahora funcione:

{% highlight bash %}
$ /path/to/android-sdk-linux/platform-tools/adb version
{% endhighlight %}

obteniendo como salida un mensaje similar a este:

{% highlight bash %}
Android Debug Bridge version 1.0.32
{% endhighlight %}

# Android Asset Packaging Tool (aapt)

Una vez hemos solucionado el problema con el Android Debug Bridge nos daremos cuenta que todavía no anda nuestra aplicación:

#### Error:

{% highlight bash %}
...error while loading shared libraries: libz.so.1: cannot open shared object file: No such file or directory
{% endhighlight %}

#### Solución:

{% highlight bash %}
$ sudo aptitude install lib32z1
{% endhighlight %}

#### Comprobamos que ahora funcione:

{% highlight bash %}
$ /path/to/android-sdk-linux/build-tools/xx.x.x/aapt version
{% endhighlight %}

obteniendo como salida un mensaje similar a este:

{% highlight bash %}
Android Asset Packaging Tool, v0.2-1635773
{% endhighlight %}

Nota:

> xx.x.x ==> versión de tu SDK, en mi caso 21.1.2

Con esto ya todo deberian andar como corresponde.


Fuente: [dandar3.blogspot.com][articulo]


[android]:  http://www.android.com/
[ubuntu]: http://www.ubuntu.com/
[sdk]: http://developer.android.com/intl/es/sdk/index.html
[articulo]: http://dandar3.blogspot.com/2014/03/android-sdk-tools-on-ubuntu-1404-beta.html
[abd]: http://developer.android.com/intl/es/tools/help/adb.html
[aapt]: http://developer.android.com/intl/es/tools/building/index.html
