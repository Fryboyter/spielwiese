---
title: NetworkManager auf iwd umstellen
date: 2021-07-31T18:33:57+0200
categories:
- Linux
- OSBN
tags:
- NetworkManager
- iwd
- WLAN
- Wpa_supplicant
slug: network-manager-auf-iwd-umstellen
---
Zum Verwalten von Netzwerkverbindungen verwenden viele Nutzer das Tool NetworkManager. Wenn es um WLAN-Verbindungen geht, kommt hierbei meist wpa_supplicant zum Einsatz. Wird die Verbindung getrennt weil der Rechner beispielsweise in den Ruhezustand versetzt wurde, dauert es relativ lange bis die Verbindung wieder aufgebaut wird. 

Um den Verbindungsaufbau zu beschleunigen kann man anstelle von wpa_supplicant [iwd](https://iwd.wiki.kernel.org) nutzen. 

Zuerst installiert man es mit der jeweiligen Paketverwaltung (in Falle von Arch Linux also mittels <mark>pacman -S iwd</mark>). Nun erweitert man die Datei /etc/NetworkManager/NetworkManager.conf um folgenden Inhalt bzw. passt die Datei entsprechend an, falls bereits ein anderes WiFi Backend definiert ist.

<pre class="line-numbers language-bash" style="white-space:pre-wrap;">
<code class="language-bash">[device]
wifi.backend=iwd</code>
</pre>

Abschließend beendet man wpa_supplicant mittels <mark>systemctl stop wpa_supplicant.service</mark> und startet NetworkManager mit <mark>systemctl restart NetworkManager.service</mark> neu. Nun sollte iwd anstelle von wpa_supplicant verwendet werden und der Verbindungsaufbau sollte von nun an schneller erfolgen.