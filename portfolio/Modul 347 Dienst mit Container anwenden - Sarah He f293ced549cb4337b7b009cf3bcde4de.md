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

![image](https://user-images.githubusercontent.com/126601670/229376300-f4e97291-e517-4f53-bf69-543165c03c66.png)

## Raft-Konsens-Algorithmus

Der Raft-Konsensalgorithmus ist ein Protokoll, das für die Verwaltung von verteilten Systemen verwendet wird, um eine gemeinsame Übereinstimmung zwischen verschiedenen Prozessen zu erzielen. Der Algorithmus ist nach dem Fluss-Rafting-Sport benannt, bei dem Teams von Menschen zusammenarbeiten, um Hindernisse auf einem Fluss zu überwinden.

In verteilten Systemen besteht das Problem darin, dass es schwierig sein kann, eine gemeinsame Übereinstimmung darüber zu erzielen, welcher Prozess was tut. Der Raft-Algorithmus löst dieses Problem, indem er eine Leader-Node auswählt, die für die Koordination aller Aktionen verantwortlich ist. Alle anderen Nodes werden Follower und akzeptieren den Status des Leader Nodes als gültigen Zustand.

Der Raft-Algorithmus bietet einige Vorteile gegenüber anderen Konsensalgorithmen wie zum Beispiel einer einfachen Implementierung, einer besseren Lesbarkeit des Codes und einer schnelleren Wiederherstellung nach einem Node-Ausfall. Es ist einer der am häufigsten verwendeten Algorithmen für die Implementierung von verteilten Systemen und wird in vielen Anwendungen wie Datenbanken, Cloud-Services und Blockchains eingesetzt.

Ein Cluster wird oft mit einer ungeraden Anzahl von Nodes eingerichtet, um die Wahrscheinlichkeit einer geteilten Abstimmung im Konsensalgorithmus zu reduzieren.

### Warum ungerade Anzahl Nodes

Bei einem verteilten System wie einem Cluster müssen sich die Nodes auf eine gemeinsame Entscheidung bezüglich des Zustands des Systems einigen. In vielen Konsensalgorithmen wird dazu eine Abstimmung durchgeführt, bei der jede Node eine Stimme hat. Wenn die Anzahl der Nodes gerade ist und es zu einer geteilten Abstimmung kommt, bei der die Stimmen gleichmäßig zwischen den Nodes aufgeteilt werden, kann es schwierig sein, eine Entscheidung zu treffen und das System kann in einen inkonsistenten Zustand geraten.

Durch die Verwendung einer ungeraden Anzahl von Nodes kann dieses Problem vermieden werden. Wenn eine geteilte Abstimmung auftritt, wird immer eine Node mehr Stimmen haben als die andere Seite, und es kann eine Entscheidung getroffen werden, die das System in einen konsistenten Zustand bringt.

Obwohl eine ungerade Anzahl von Nodes das Problem der geteilten Abstimmung reduziert, ist es nicht immer eine Garantie dafür, dass das System in jedem Fall korrekt funktioniert. Es gibt andere Faktoren wie Netzwerkprobleme oder unerwartete Ausfälle, die ebenfalls zu inkonsistenten Zuständen führen können.

### Wie wird der leader gewählt?

Im Raft-Konsensalgorithmus wird der Leader durch einen Wahlprozess gewählt. Dieser Wahlprozess beginnt in der Regel, wenn ein Follower-Node keinen Kontakt mehr zum aktuellen Leader hat. Der Follower startet dann eine Wahl und sendet eine Request Vote-Nachricht an alle anderen Nodes im System.

Die anderen Nodes prüfen, ob sie bereits für einen anderen Kandidaten gestimmt haben. Wenn sie das noch nicht getan haben, stimmen sie für den Kandidaten. Um gewählt zu werden, muss ein Kandidat mindestens die Hälfte der Stimmen der Nodes im System erhalten. Wenn ein Kandidat diese Mehrheit erhält, wird er zum neuen Leader ernannt und sendet eine Heartbeat-Nachricht an alle anderen Nodes, um seine Autorität zu etablieren.

Wenn kein Kandidat eine Mehrheit erhält, wird der Wahlprozess wiederholt. In diesem Fall wird jedoch eine zufällige Wartezeit vor der Wahl eingeführt, um zu verhindern, dass es zu einer Endlosschleife kommt, in der sich die Nodes immer wieder gegenseitig wählen, ohne dass ein Leader bestimmt wird.

## Kubernetes Abb

ABB (Atomic Broadcast Protocol) ist ein Protokoll, das zur Koordination von Aktivitäten zwischen den Nodes in einem Kubernetes-Cluster verwendet wird. Es wird normalerweise im Rahmen von Kubernetes verwendet, um sicherzustellen, dass Änderungen am Cluster-Status von allen Nodes im Cluster einheitlich und atomar umgesetzt werden.

Die Implementierung von ABB in Kubernetes erfolgt über den Raft-Konsensalgorithmus, der von der Control Plane verwendet wird, um den Cluster-Status zu verwalten. Die Control Plane besteht aus mehreren Komponenten wie dem API Server, dem Scheduler, dem Controller Manager und dem etcd-Cluster.

Das etcd-Cluster ist ein verteiltes Key-Value-Store-System, das von der Control Plane verwendet wird, um den Cluster-Status und die Konfigurationsinformationen zu speichern. Jeder Node im Kubernetes-Cluster hat eine lokale Kopie des etcd-Clusters, um schnell auf Änderungen reagieren zu können.

Sobald ein Node im Cluster einen Änderungsantrag stellt, wird der Antrag an den API Server gesendet. Der API Server prüft dann, ob der Änderungsantrag gültig ist, und leitet ihn an den etcd-Cluster weiter, der die Änderung in seinen lokalen Speicher schreibt. Wenn der etcd-Cluster die Änderung akzeptiert hat, sendet er eine Bestätigungsnachricht an den API Server, der die Änderung an alle anderen Nodes im Cluster weitergibt.

Jeder Node im Cluster erhält die Änderung vom API Server und aktualisiert seinen lokalen Status entsprechend. Der Raft-Konsensalgorithmus gewährleistet, dass jeder Node im Cluster denselben Status hat, indem er sicherstellt, dass Änderungen atomar und konsistent umgesetzt werden.

Durch diese Implementierung von ABB über den Raft-Konsensalgorithmus kann Kubernetes sicherstellen, dass der Cluster-Status atomar und konsistent ist, und so die Zuverlässigkeit und Verfügbarkeit des Clusters verbessern.

## Dashboard

    microk8s dashboard-proxy
    
Anschliessend die ausgegebene IP zum zugreifen verwenden und den Token dazu eingeben

![image](https://user-images.githubusercontent.com/126601670/229377005-4c3cef67-c3f2-4f9f-92cc-07b70a6127cb.png)


## Self Healing
In Kubernetes hat man die möglichkeit mit einem Controll Plane Prozess den Cluster quasi unsterblich zu machen. Dabei Konfiguriert man einen Deployment Controller so, dass er den Cluster beobachtet und bei einer Abweichung die problematischen Pods wieder startet: spec: replicas:3 im yaml file.

## Scale-Up / Scale-Down

Mit Kubernetes hat man die Option, seine Cluster einfach zu skallieren. Dafür kann man entweder einen Befehl eingeben, welchen ich unten aufgeführt habe oder mann hat die Möglichkeit das ganze Persistent in die Config Datei zu schreiben, damit dies bei einer aktualisierung der Version vorhanden bleibt. So kann man erkennen, wenn man einen zu grossen oder zu kleinen Workload hat, und anschliessend ein Scale Up oder Scale Down vornehmen. Zudem besteht mit Kubernetes neuerding die möglichkeit, automatic horizontal autoscaling zu verwenden, wodurch der Cluster selbst merkt, wann die Last zu gross bzw. zu klein ist und anschliessend automatisiert Pods repliziert.

## Rolling Update

        microk8s kubectl apply -f "Pfad zu deploy v2"
        
![image](https://user-images.githubusercontent.com/126601670/229377072-ad6e4f77-9049-4a84-b44d-3c572a414dc4.png)


## Blue-Green Deployment

Blue-Green Deployment ist ein Konzept der Entwicklung, bei dem das Zerodowntime konzept erhalten wird, indem man die neue Version der Umgebung (Green) parrallel zu der alten (Blue) startet und den Datenverkehr erst dann auf die neue Leitet, wenn diese bereit dazu ist. Anschliessend kann die Alte Version aus dem Cycle genommen werden.

## Eigene Notitzen

### Master Nodes

Sollten immer 3 bis 5 vorhanden sein in verschiedenen Räumen, um die Hochverfügbarkeit zu gewährleisten, da die Masters das Gehirn des Clusters sind.

Aufgaben: 
API Server
Scheduler
Key/Value-Store
Cloud Controller

![image](https://user-images.githubusercontent.com/102524498/225909289-1ad71147-30d6-45db-849b-4df54f6b0872.png)

Im Kubernetes-Cluster gibt es verschiedene Komponenten, die jeweils unterschiedliche Aufgaben haben. Der API-Server dient als direkte Schnittstelle für Benutzer, um Befehle an den Cluster zu senden und Antworten vom Server zu empfangen.

Der Scheduler ist für die Auswahl der Nodes verantwortlich, auf denen die Nutzeranwendungen ausgeführt werden sollen. Der Key/Value-Store speichert den aktuellen Zustand des Clusters sowie aller Anwendungen.

Der Controller Manager überwacht die Aktivitäten im Cluster und führt verschiedene Aufgaben aus, wie zum Beispiel Reparaturen von fehlerhaften Containern oder Neustarts von abgestürzten Containern.

Der Cloud Controller ermöglicht es Kubernetes, sich mit Cloud-Services wie Speicher- und Lastenausgleichsdiensten zu integrieren


### Worker Nodes
Die Nodes im Kubernetes-Cluster sind dafür verantwortlich, die Nutzeranwendungen auszuführen und können entweder unter Linux oder Windows betrieben werden. Während Linux Nodes nur Linux-Anwendungen ausführen können, sind Windows Nodes auf die Ausführung von Windows-Anwendungen spezialisiert.

Die Worker Nodes im Cluster sind in der Regel größer und benötigen mehr Ressourcen als die Master Nodes, da sie alle Anwendungen ausführen. Jeder Node verfügt über verschiedene Services wie den Kubelet, der als Agent des Clusters fungiert und mit der Control-Plane kommuniziert, um Aufgaben zu empfangen und den Status der ausgeführten Aufgaben zu melden. Die Container-Runtime ist ein weiterer wichtiger Service, der Container startet und ausführt.

![image](https://user-images.githubusercontent.com/102524498/225914230-93b3fa16-dc37-4f34-b43b-851249f1697c.png)


## Wichtige Befehle

    microk8s start 
    microk8s status --wait-ready
    microk8s enable dashboard dns registry ingress
    microk8s kubectl get nodes
    microk8s kubectl cluster-info
    microk8s enable metallb

    Sie werden nach einem IP Range gefragt. Geben Sie hier die IP Ihres Clusters ein. Im Beispiel oben: 172.20.153.220-172.20.153.240
    
    microk8s kubectl get componentstatus
    microk8s kubectl create -f "Pfad"
    microk8s kubectl get rc
    microk8s kubectl apply -f todo-app-deploy-v2.yaml
    microk8s kubectl scale --replicas 2 deployment/todo-app-deployment

## Node IP

Die Node IP ist eine Adresse einer physischen oder virtuellen Maschine, welche eine Node Rolle im Cluster hat. Dabei ist die Adresse die gleiche wie die der Netzwerkkarte. Die Node IP wird meist als External IP verwendet, um von ausserhalb auf einen Service zuzugreifen.

## Cluster IP

Die Cluster IP ist eine virtuelle IP-Adresse, welche einem Service zugeordnet ist. Sie wird dazu verwendet, um auf den Service innerhalb des Clusters zuzugreifen. Die interne Kommunikation läuft darüber ab.

## LoadBalancer

Ein Kubernetes-Loadbalancer ist ein Typ von Service, der dazu beiträgt, den Netzwerkverkehr über mehrere innerhalb eines Kubernetes-Clusters ausgeführte Pods zu verteilen. Er fungiert als Vermittler zwischen eingehenden Anfragen und den Pods und stellt sicher, dass jeder Pod einen fairen Anteil des Verkehrs erhält. Kubernetes-Loadbalancer bieten eine zuverlässige Möglichkeit, Anwendungen zu skalieren, indem sie die Weiterleitung des Netzwerkverkehrs automatisch an die verfügbaren und gesunden Pods anpassen. Loadbalancer können auf verschiedene Arten konfiguriert werden, wie z.B. mit Round-Robin- oder Least-Connection-Algorithmen, und können auch TLS-Terminierung und Sitzungspersistenz unterstützen. Durch die Verwendung eines Kubernetes-Loadbalancers können Organisationen sicherstellen, dass ihre Anwendungen hochverfügbar bleiben und auf Benutzeranfragen reagieren.

## Namepsaces

Ein Kubernetes Namespace ist ein virtueller Cluster innerhalb eines Kubernetes-Clusters, der dazu dient, Objekte wie Pods, Services und Deployments voneinander zu isolieren. Ein Namespace stellt eine logische Gruppierung von Ressourcen dar und ermöglicht es mehreren Teams, Anwendungen oder Arbeitslasten auf einem Kubernetes-Cluster zu betreiben, ohne dass sie sich gegenseitig beeinträchtigen oder stören.
Ein Namespace kann auch dazu verwendet werden, um verschiedene Umgebungen wie Entwicklung, Testen und Produktion voneinander zu trennen, indem sie unterschiedliche Namensräume verwenden, um sicherzustellen, dass die Anwendungen in jeder Umgebung getrennt sind und nicht versehentlich in einer anderen Umgebung deployt werden.
Standardmäßig wird jede Kubernetes-Installation mit einem Default-Namespace geliefert, in dem sich alle Objekte ohne explizite Zuordnung befinden. Wenn man ein Objekt ohne Angabe des Namespaces erstellt, wird es automatisch in diesem Default-Namespace erstellt.


## Printscreens -------
![image](https://user-images.githubusercontent.com/126601670/229377383-c55bb532-623c-47ae-8f8f-31330a4c5fe6.png)


![image](https://user-images.githubusercontent.com/126601670/229377408-5c4dad11-9d3e-46b1-a062-7120d18ba1ef.png)
