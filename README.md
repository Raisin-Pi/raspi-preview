Version alpha VNC pour Raspberry Pi
==========================

[![Minecraft Pi GIF animé](MinecraftPi.gif)](http://www.youtube.com/watch?v=nMhjg7GdRWY "Vidéo Pi")

*Cliquez sur l'image ci-dessus pour une vidéo supplémentaire de Minecraft via VNC.*

Merci pour votre aide en testant cette version alpha VNC pour Raspberry Pi ! Cette version contient tout un ensemble d'améliorations par rapport à notre [version stable](https://www.realvnc.com/download/vnc/raspberrypi/), y compris support pour Minecraft, la possiblité de restituer à l'écran le terminal texte du Pi, ainsi que des performances améliorées pour tous les modèles du Pi. 

**Télécharger la version alpha 1 maintenant à partir des [Sous-versions GitHub](https://github.com/RealVNC/raspi-preview/releases/download/5.3.1.18206/VNC-Server-5.3.1-raspi-alpha1.deb)**

La version alpha est fournie automatiquement sous [licence Personelle](https://www.realvnc.com/products/vnc/#versions) qaund vous l'installer sur votre Raspberry Pi (mais n'hésitez pas d'y ajouter une clé de "licence Enterprise" vous-même pour des fonctionnalités supplémentaires). La validité de la licence alpha se termine fin Janiver 2017.

Puisqu'il s'agit d'un test alpha, vous pourriez éventuellement remarquer quelques anomalies. Une liste de [problèmes connus](#knownIssues) et des instructions pour pouvoir [faire un retour d'expérience](#leavingFeedback) sont inclues à la fin de ce document "*Readme*".

N'oubliez pas que vous avez besoin du [Client VNC](https://www.realvnc.com/download/viewer/) sur la machine que vous utilisez pour contrôler votre Pi. 

**Note:** Vous aurez besoin de procéder à une [optimization du client VNC](#optimizingVncViewer) afin de profiter des meilleures performances de cette version alpha.

<a name="releaseNotes"></a>

Notes de Version
=============

- **NEW:** Minecraft can now be played on the Raspberry Pi over VNC ([Service Mode](#startVnc) only).
- **NEW:** The Raspberry Pi's text console can now be accessed over VNC (Service Mode only). 
- **NEW:** Any program which uses a directly rendered overlay (e.g. Kodi, the Pi camera's preview window, omxplayer etc.) can now be used on the Pi over VNC (Service Mode only).  
- **NEW:** VNC Server now uses hardware acceleration on all Pi models, ensuring a faster, smoother experience.  


Prerequisites
=============

- Ensure your Pi is running Raspbian. 
- Ensure you are using your Pi's [recommended power supply](https://www.raspberrypi.org/help/faqs/#powerReqs). 
- For optimal performance, increase your Pi's GPU allocation to at least 128mb (this is 64mb by default). You can do this by running ``sudo raspi-config`` in Terminal and selecting **Advanced options > Memory Split**. 


Installation
============

[Download the VNC Server package from GitHub Releases](https://github.com/RealVNC/raspi-preview/releases/download/5.3.1.18206/VNC-Server-5.3.1-raspi-alpha1.deb), and install using `dpkg` or your favourite package manager. 

e.g. from the command line:
```
curl -OL https://github.com/RealVNC/raspi-preview/releases/download/5.3.1.18206/VNC-Server-5.3.1-raspi-alpha1.deb
sudo dpkg -i VNC-Server-5.3.1-raspi-alpha1.deb
```

You can then [start VNC Server](#startVnc) at the command line. 

You can use the [latest VNC Viewer for your platform](http://www.realvnc.com/download/viewer/), although you may need to [optimize the configuration](#optimizingVncViewer).

<a name="startVnc"></a>

Starting VNC Server
===================

You can run VNC Server in two modes: Service Mode and Virtual Mode. You can even run both at the same time. For more information, see [here](https://www.realvnc.com/products/vnc/raspberrypi/). 

**Note:** Only Service Mode will be able to capture Minecraft and similar applications.

Raspbian "Jessie"
-----------------
To run VNC Server in Service Mode:
```
sudo systemctl start vncserver-x11-serviced.service
```
To have VNC Server start automatically when you power the Pi on:
```
sudo systemctl enable vncserver-x11-serviced.service
```

Raspbian "Wheezy"
-----------------
To run VNC Server in Service Mode:
```
sudo /etc/init.d/vncserver-x11-serviced start
```
To have VNC Server start automatically when you power the Pi on:
```
sudo update-rc.d vncserver-x11-serviced defaults
```

Additional instructions, including how to connect a VNC Viewer device and how to stop VNC Server, are available [here](https://www.realvnc.com/products/vnc/raspberrypi/). 

<a name="optimizingVncViewer"></a>

Optimizing VNC Viewer for the Raspberry Pi
==========================================

To make the most of VNC Server's hardware acceleration, configure VNC Viewer in the following way: 

1. Run VNC Viewer and connect to the Raspberry Pi. 
2. On the VNC Viewer toolbar, click the **Options** button. 
3. Click **Advanced...**, then the **Expert** tab. 
4. Set ``PreferredEncoding`` to ``JPEG``, ``AutoSelect`` to ``False``, and ``ColorLevel`` to ``Full``. 

Playing Minecraft
=================

To play Minecraft over VNC: 

1. Run VNC Server in Service Mode on your Pi and connect to it with VNC Viewer. 
2. On your VNC Viewer device, press the F8 key and ensure **Relative Pointer Motion** is checked. 
3. Start and play Minecraft, as if you were sitting in front of the Pi. 
5. When you finish playing, press F8 and uncheck **Relative Pointer Motion**. 

![Minecraft VNC](Screenshot1.PNG)

Running Kodi
============

To use Kodi over VNC: 

1. Run VNC Server in Service mode on the Pi and connect to it with VNC Viewer. 
2. On your VNC Viewer device, press the F8 key and ensure **Relative Pointer Motion** is checked. 
2. Press Ctrl Alt F2 to access the Pi's console. 
3. Run ``kodi``. 
4. Use Kodi, as if you were sitting in front of the Pi. 
5. When you finish using Kodi, exit in the usual way. Then press F8 and uncheck **Relative Pointer Motion**. 

![KodiVNC](KodiScreen.PNG)

<a name="knownIssues"></a>

Known issues
============

- Kodi only accepts keyboard input over VNC when it is started by running ``kodi`` at the Raspberry Pi's console. 
- Connecting to a headless Pi may result in VNC Viewer's **Options** dialog being cut off. [Increase the Pi's default resolution](https://support.realvnc.com/knowledgebase/article/View/523) to fix. 

For an up-to-date list of known issues, please click [here](https://github.com/RealVNC/raspi-preview/issues). 

<a name="leavingFeedback"></a>

Leaving feedback
================

We'd love to hear your thoughts! If you have any feedback, or if you've spotted a bug, please let us know through GitHub's [issue reports](https://github.com/RealVNC/raspi-preview/issues) page. You can also tweet us [@RealVNC](https://twitter.com/RealVNC) or email us at [raspi@realvnc.com](mailto:raspi@realvnc.com).

Thanks for your help. 
