# Workshop Inhalt
	- Wie kann eine Anwendung resilient betrieben werden, damit sie auch nach Abstürzen weiterhin verfügbar ist?
	- Kennenlernen von drei Deployment-Strategien, Rolling Update, Blue/Green und Canary Deployment.
	- ![deployment-strategien-meme.gif](../assets/deployment-strategien-meme_1700573806500_0.gif)
	- ## Quellen
	  [Learn Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
	  [Learn Kubernetes Basics (Interactive)](https://kubernetes.io/docs/tutorials/kubernetes-basics/explore-interactive/)
- # Installation und Wartung
	- ## Ausgangssituation
	  Anwendung läuft auf Server. Sie benötigt ein Betriebssystem, Bibliotheken (z.B. für DB-Zugriff)
	  und evtl. Laufzeitumgebungen wie Java Runtime, Node.JS, Python, ...
	- ## Installation
		- <p style="text-align: left"><ul><li>Betriebssystem, Bibliotheken und Laufzeitumgebungen</li>
		  <li>Anwendung selbst</li>
		  <li>Die notwendigen Schritte müssen exakt ausgeführt werden oder automatisiert werden, z.B. mit Ansible</li>
		  </ul></p>
		- Als Entwickler*in möchte ich die Anwendung auf meinem Rechner installieren können, um sie zu testen.
		- Bei so vielen Komponenten kann ein Versionsunterschied oder eine Abweichung bei der Installation dazu führen, dass die Anwendung nicht mehr läuft.
		- Auf dem Server laufen evtl. weitere Anwendungen, wodurch Konflikte entstehen könnten.
	- ## Wartungsaufgaben
		- Updates oder Security-Patches des Betriebssystems, der Laufzeitumgebung oder der Anwendung selbst müssen regelmäßig installiert werden.
		- Die Updates sollen während des Betriebs installiert werden, ohne dass die Anwendung ausfällt.
- # Lösungsbausteine
	- ## Images / Container
		- Alle benötigten Dateien sollen unveränderlich *eingefroren* werden.
		- <p style="text-align: left"><ul><li>Images enthalten alle notwendigen Komponenten, um die Anwendung auszuführen. Sie sind unveränderlich, wie ISO-Images.</li>
		  <li>Images sind Vorlagen für die Erstellung von Containern.</li>
		  <li>Container sind leichtgewichtige, portable Einheiten für Software.</li>
		  <li>Sie sind von der zugrundeliegenden Infrastruktur isoliert.</li></ul></p>
		- ![](https://nesi.github.io/nzrse-containers/fig/container_vs_vm.png)
- # Setup
	- <p style="text-align: left">'git' installiert?</p>
	  ```shell
	  sudo apt install git
	  ```
	- <p style="text-align: left">Workshop-Repo klonen</p>
	  ```shell
	  git clone https://github.com/stefan-niemeyer/k8s-workshop.git
	  ```
	- <p style="text-align: left">K8s Rechte kopieren</p>
	  ```shell
	  cd
	  mkdir .kube
	  cd .kube
	  sudo cp /etc/rancher/k3s/k3s.yaml config
	  sudo chown k3s:k3s config
	  cd
	  ```
	- <p style="text-align: left">'.bashrc' erweitern</p>
	  ```shell
	  nano .bashrc
	  ```
	  [:br]
	  <p style="text-align: left">Zeilen eintragen</p>
	  ```shell
	  export KUBECONFIG=$HOME/.kube/config
	  alias k=kubectl
	  ```
	  [:br]
	  <p style="text-align: left">Neuer Tab oder 'source .bashrc' ausführen</p>
- Blue Green https://kubernetes.io/blog/2018/04/30/zero-downtime-deployment-kubernetes-jenkins/
