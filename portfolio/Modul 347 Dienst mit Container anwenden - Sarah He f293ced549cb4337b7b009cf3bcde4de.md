# Modul 347 Dienst mit Container anwenden - Sarah Hergott INF2021F - 28.02.2023

![Download (1).png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/Download_(1).png)

# **Beschreibung Container**

---

Mithilfe von Container können Applikationen sowie auch abgespeckte Betriebssysteme virtualisiert werden. Dabei wird jedoch nicht die Hardware virtualisiert, wodurch Rechenleistung eingespart werden kann. Mithilfe von Containern kann man die genannten Objekte sehr schnell deployen, dafür kommen meist Vorlagen wie Docker Compose Files oder Ähnliches zur Verfügung. Es besteht auch die Möglichkeit, Cluster zu erstellen (z.B. Kubernetes) womit man eine Hochverfügbarkeit und eine hohe Skalierbarkeit der Containerdiensten sicherstellen kann.

# **DevOps**

---

DevOps ist eine Idee, in welcher man mithilfe von passenden Praktiken und Tools die Entwicklung, den Betrieb und die Qualitätssicherung in einem Knoten zusammenführt. So besteht ein DevOps-Team aus den Entwicklern sowie auch aus den Betreibern eines Software-Objektes, wodurch ein qualitatives und schnelles Software-Deployment sichergestellt werden kann.

# **Virtualisierung vs. Containerisierung**

---

## **Virtualisierung**

Bei der Virtualisierung werden benötigte Hardware Ressourcen für den Betrieb eines Betriebssystems virtualisiert bereitgestellt. Dabei können auch Parameter übergeben werden, dass das Betriebssystem gar nicht merkt, dass es virtualisiert läuft. Dies bringt vor allem im Microsoft-Bereich Vorteile, da Windows Probleme bereiten kann aufgrund von nicht akzeptieren der virtualisierten Hardware.

### **Hypervisor**

Bei der Virtualisierung kommen Hypervisoren ins Spiel, welche die benötigten Ressourcen zum virtualisieren bereitstellen. Es gibt verschiedene Arten von Hypervisoren, welche auf verschiedenen Ebenen eines Computers arbeiten. So arbeitet KVM direkt auf dem Kernel, welcher KVM eine direkte Verbindung zu den Ressourcen bereitstellt. Dabei bekommt KVM einen Anteil des Kernels, welcher natürlich von den anderen Teilen abgeschottet ist. Hingegen wird bei Hypervisoren wie Virtualbox auf dem Betriebssystem virtualisiert, sodass das Betriebssystem die Vermittlung der Hardware abschließt. Dabei wird die Geschwindigkeit etwas reduziert, jedoch wird die Anwendung um einiges intuitiver.

## **Containerisierung**

Wie bereits erwähnt wird bei der Containerisierung keine Harware virtualisiert. Es wird lediglich mit einer Containerengine Software Virtualisiert, welche auch abgeschottet vom restlichen System ist. Dadurch dass nur Software virtualisiert wird, kann man den Overhead einsparen und zudem viel schneller ein Deployment machen, welches innert Sekunden gestartet ist.

![play-with-docker.png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/play-with-docker.png)

# Image vs. Container

---

Ein Image ist eine Datei, welche die benötigten Bibliotheken und Parameter zur Erstellung eines Containers bereitstellt wobei es sich bei einem Container um die laufende Umgebung handelt, welche durch diese Bibliotheken und Parameter erstellt wurde.

# Befehle für Docker Images

---

docker image (parameter):

```docker
build – Erstellt ein Image.
push – Schiebt ein Image auf eine Remoteregistrierung.
pull – Zieht ein Image oder ein Repository von einer Registry.
ls – Listet alle vorhandenen Images auf.
history – Zeigt alle Informationen eines Intermediate Image an.
inspect – Zeigt detaillierte Informationen zu einem Image an, inkl. den einzelnen Layern.
rmi – Löscht ein Image.
```

# Befehle für Docker Container

---

docker container (parameter):

```docker
create – Erstellt einen Container aus einem Image.
start – Startet einen existierenden Container.
run — Erstellt einen neuen Container und startet ihn.
ls – Listet alle laufenden Container auf.
inspect – Zeigt detaillierte Informationen über einen Container an.
logs – Druckt logs aus.
stop – Stoppt einen laufenden Container.
kill – Stoppt den Hauptprozess in einem Container abrupt.
rm – Löscht einen gestoppten Container.
```

# Weitere nützliche Docker Befehle

---

```docker
docker version – Zeigt die Docker Version von Echo-Client und Server an.
docker images – Listet alle Docker Images auf.
docker save <path> <image> – Speichert ein Docker Image in eine .tar-Datei, die durch „path“ näher spezifiziert ist.
docker export – Exportiert das Dateisystem eines Containers als tar-Archiv.
docker exec – Führt einen Befehl in einem laufenden Container aus.
docker ps -a – Zeigt alle Container an (das -a steht für das Flag –all).
docker ps -l – Zeigt den letzten erstellten Container an.
docker search – Durchsucht das Docker Hub nach Images.
docker attach – Hängt etwas an einen laufenden Container an.
docker commit – Erstellt ein neues Image mit den Änderungen, die an einem Container vorgenommen worden sind.
```

# Onlyoffice Screenshot

---

![onlyoffice-screenshot.png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/onlyoffice-screenshot.png)

# Docker Applikation erstellen

---

## Dockerfile

In einem Dockerfile werden alle Argumente gesetzt, welche es zum Erstellen eines Images benötigt. Dies kann wie folgt aussehen:

```docker
FROM alpine:3.16.2
MAINTAINER Johannes M. Scheuermann <johannes.scheuermann@inovex.de>

COPY ./bin/todo-app /app/todo-app
COPY ./public /app/public
RUN chmod +x /app/todo-app
WORKDIR /app
CMD ["./todo-app"]
EXPOSE 3000
```

## Image

Mit folgendem Befehl kann ein Image ertsellt und getagged werden:

```docker
docker image build -t "TAG" "Verzeichniss"
```

## **Docker network**

Mit Docker network kann man Containernetzwerke erstellen:

```docker
docker network create "Netztwerkname"
```

Diese Netzwerke kann man anschliessend beim Run Befehl übergeben.

## Docker run

Mit folgendem Befehl können die Images gestartet werden, wobei man verschiedene Flags angeben kann:

```docker
docker run --net=Netzwerkname --name=Containername -d (-p port:port) "Imagename"
Flags:
--restart unless-stopped (Bei fehler neustarten)
```

## **Docker Image pushen**

```docker
docker login
```

Einloggen

```docker
docker image tag "Imagename" "Neuer name mit username/ vornedran"
docker image push "Imagename"
docker logout
```

Nun sollte eine Checksumme des Images erscheinen.

Wenn man sich jetzt in seinem Dockerhub einloggt online sollte unter Repositories das bzw. die Images erscheinen:

![221901152-6300f648-a48e-4e66-a411-e972735b0412.png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/221901152-6300f648-a48e-4e66-a411-e972735b0412.png)

# Neue Version erstellen

---

```docker
gitclone "URL zu Sourcecode der neuen version"
cd "Verzeichnis"
docker image build -t "Reponamen von alter version:v2"
docker login
docker image push "Imagename"
docker logout
```

Anschliessend sollte das neue V2 Image im selben Repo wie das alte Image erscheinen:

![221902763-02a127d2-1cb4-4d17-acc3-76ee446221a2.png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/221902763-02a127d2-1cb4-4d17-acc3-76ee446221a2.png)

# Andere Befehle

---

Bereinigen vom Docker System (Wichtig: nur wenn alles Wichtige in Registry gespeichert wurde): docker system prune --all --volumes

![219610831-c9ada056-da15-44a3-8be3-152a2dd5a3df (1).png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/219610831-c9ada056-da15-44a3-8be3-152a2dd5a3df_(1).png)

![219610933-2e366e54-e69a-431b-b5ca-000a6d5c69e6 (1).png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/219610933-2e366e54-e69a-431b-b5ca-000a6d5c69e6_(1).png)

# Docker Compose

---

Docker Compose ist ein Tool, welches dabei hilft, mehrere verbundene Container eines Stacks in einem Befehl zu starten. So ist es einfacher, komplexe Applikationen mit anderen zu teilen und anschliessend zu starten. Anstatt mühsam mit Run alle Container einzeln zu starten, kann man diese in einem Docker-Compose.yml File zusammenführen und mit den richtigen Parametern ausstatten, sodass nur noch mithilfe des Compose Befehls diese Datei gestartet werden muss.

# **Version 2 der App mit Compose**

---

## Compose File

nano ./docker-compose.yml

Eintragen mit eigenem Repo für die Images (username/image):

```docker
version: "3"
 services:

   todoapp:
     container_name: todo-app
     image: she136239/todo-app:v2
     networks:
      - todoapp_network
     ports:
      - "3000:3000"
     depends_on:
      - redis-master
      - redis-slave

   redis-slave:
     container_name: redis-slave
     image: she136239/redis-slave:v1
     networks:
      - todoapp_network
     depends_on:
      - redis-master

   redis-master:
     container_name: redis-master
     image: she136239/redis-master:v1
     networks:
       - todoapp_network

 networks:
   todoapp_network:
```

# **Applikation starten und verwenden**

---

```docker
docker compose up -d
```

Die App kann nun im Browser über den Port 3000 erreicht werden.

# App Version 2 via Portainer starten

---

Im Browser über Port 9000 zugreifen und anschliessend im reiter Stacks den compose Inhalt einfügen und den Stack starten:

![221904685-64f79090-7ced-47e2-b636-415b744a8ac3.png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/221904685-64f79090-7ced-47e2-b636-415b744a8ac3.png)

# Sock Shop

---

Vorgehen:

```docker
git clone https://github.com/microservices-demo/microservices-demo
    cd microservices-demo
    
    docker-compose -f deploy/docker-compose/docker-compose.yml up -d
```

Nun ist die Demo erreichbar

Im Portainer sieht die App wie folgt aus:

![221427456-041c406b-a298-49bf-af89-57451fe2fa6a.png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/221427456-041c406b-a298-49bf-af89-57451fe2fa6a.png)

# Eigenes Projekt

---

# Vorgehen

---

```docker
mkdir Wordpress
cd Wordpress
nano docker-compose.yml
```

Eintragen: 

```docker
services:
      db:
        # We use a mariadb image which supports both amd64 & arm64 architecture
        image: mariadb:10.6.4-focal
        # If you really want to use MySQL, uncomment the following line
        #image: mysql:8.0.27
        command: '--default-authentication-plugin=mysql_native_password'
        volumes:
          - db_data:/var/lib/mysql
        restart: always
        environment:
          - MYSQL_ROOT_PASSWORD=somewordpress
          - MYSQL_DATABASE=wordpress
          - MYSQL_USER=wordpress
          - MYSQL_PASSWORD=wordpress
        expose:
          - 3306
          - 33060
      wordpress:
        image: wordpress:latest
        ports:
          - 8000:80
        restart: always
        environment:
          - WORDPRESS_DB_HOST=db
          - WORDPRESS_DB_USER=wordpress
          - WORDPRESS_DB_PASSWORD=wordpress
          - WORDPRESS_DB_NAME=wordpress
      redirect:
        image: she136239/redirect:v1
        ports:
          - 80:80
        restart: always
    volumes:
      db_data:
```

# Eigenes Image

---

## Dockerfile erstellen

```docker
nano Dockerfile
```

Eintragen:

```docker
FROM nginx:alpine
    COPY . /usr/share/nginx/html
```

Anschliessend:

```docker
nano index.html
```

Eintragen:

```docker
<!DOCTYPE html>
    <html>
        <head>
            <title>Falscher Port</title>
        </head>
        <body> 
            <p>Um die Wordpress seite zu erreichen, verwende Port 8000</p>
        </body>
    </html>
```

## Printscreen von Repo

![221911466-af708be3-290d-40d3-af37-afc86fa32041.png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/221911466-af708be3-290d-40d3-af37-afc86fa32041.png)

# Projekt starten

---

```docker
docker compose up -d
```

Im Browser

```docker
http://localhost
```

![221441134-77e2bd21-d7fc-417f-9954-ca09f4a794e8.png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/221441134-77e2bd21-d7fc-417f-9954-ca09f4a794e8.png)

```docker
http://localhost:8000
```

![221441163-fa22bc8a-8536-49a5-a5fd-716bef655944.png](Modul%20347%20Dienst%20mit%20Container%20anwenden%20-%20Sarah%20He%20f293ced549cb4337b7b009cf3bcde4de/221441163-fa22bc8a-8536-49a5-a5fd-716bef655944.png)

## Kubernetes

Kubernetes ist eine Open-Source-Plattform, welche das einfache Verwalten von Containerlasten wie containerisierten Applikationen ermöglicht. Auch erleichtert Kubernetes das automatisierte starten von Stack Services. Auch bietet Kubernetes eine containerzentrale Managementumgebung.

## Microservices

Microservices ist eine Art bzw. Archidektur der Anwendunsentwicklung. Dabei wird eine Anwendung in kleine unabhängige Services unterteilt, welche über API's zusammen kommunizieren. Dabei resultiert der Vorteil, das einzelne Services gewartet bzw. verändert werden können, ohne das die ganze Anwendung darunter leidet oder nicht mehr funktioniert. Auch können Entwickler erweiterungen schnell und unkompliziert einbauen.

## Lightweightkubernetes Vergleich

|                      | Minikube | K3s      | MicroK8s  | 
| --------             | -------- | -------- | --------  | 
| Entwickler           | Kubernetes projekt   | Rancher  | Canonical    | 
| Installation   | Sehr Einfach   | Einfach   | Einfach    | 
| Modularität          | Tief     | Mittel   | Hoch      | 
| Multinode Clustering | Einfach  | Schwierig| Einfach   | 
| IOT                  | Nein     | Ja       | Ja        | 
| Production deployment| Nein     | Ja       | Ja        | 

## MicroK8s Installation

    sudo usermod -a -G microk8s $USER
    sudo chown -f -R $USER ~/.kube
    sudo chown -f -R $USER ~/.kube
    SU - $USER

Prüfen:

    microk8s status --wait-ready


Nach Lens Installation sollte MicroK8s in Lens angezeigt werden:
