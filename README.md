# Remote Desktop connection to Linux Mint 19 Cinnamon

1. Install xrdp and tiger vnc server  
    `sudo apt install xrdp tigervnc-standalone-server`

2. start xrdp  
    `sudo systemctl enable xrdp`

3. go to xrdp settings  
    `cd /etc/xrdp`

4. make copy of current settings (to recover if something will go wrong)  
    `cp xrdp.ini xrdp.ini.old`

5. update settings with new value  
    * start patching `xrdp.ini` file:  
        `cat <<EOF | sudo patch -p0`
    * paste below code and hit enter:
    ```
    --- xrdp.ini.orig       2018-07-11 14:22:02.852103588 +0900
    +++ xrdp.ini    2018-07-11 14:23:30.978905479 +0900
    @@ -153,6 +153,16 @@ tcutils=true
     ; Some session types such as Xorg, X11rdp and Xvnc start a display server.
     ; Startup command-line parameters for the display server are configured
     ; in sesman.ini. See and configure also sesman.ini.
    +[Xvnc]
    +name=Xvnc
    +lib=libvnc.so
    +username=ask
    +password=ask
    +ip=127.0.0.1
    +port=-1
    +#xserverbpp=24
    +#delay_ms=2000
    +
     [Xorg]
     name=Xorg
     lib=libxup.so
    @@ -172,16 +182,6 @@ port=-1
     xserverbpp=24
     code=10

    -[Xvnc]
    -name=Xvnc
    -lib=libvnc.so
    -username=ask
    -password=ask
    -ip=127.0.0.1
    -port=-1
    -#xserverbpp=24
    -#delay_ms=2000
    -
     [console]
     name=console
     lib=libvnc.so
    EOF
    ```

6. Done, you can restart computer.
7. Connect to your Mint machine using **Xorg** as session type.

Source:  
<https://www.hiroom2.com/2018/07/11/linuxmint-19-xrdp-cinnamon-en/>
    