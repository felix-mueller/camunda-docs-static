---

title: 'Download and Installation'
weight: 10

menu:
  main:
    name: "Download and Installation"
    parent: "get-started-language-agnostic"
    identifier: "get-started-language-agnostic-install"
    pre: "Install the Camunda BPM Platform and Camunda Modeler on your machine."

---

First you need to set up your development environment and install the Camunda BPM Platform and the Camunda Modeler.


# Prerequisites

Make sure you have the following set of tools installed:

* Java JDK 1.8,
* A modern web browser (recent Firefox, Chrome, Microsoft Edge or Internet Explorer 11 will work fine) <-- do we need this?


# Camunda BPM Platform

First, download a distribution of the Camunda BPM platform. You can choose from different distributions for various application servers. In this tutorial, we will use the Apache Tomcat based distribution. Download it from [the download page](https://camunda.com/download).

After having downloaded the distribution, unpack it inside a directory of your choice.

After you have successfully unpacked your distribution of the Camunda BPM platform, execute the script named `start-camunda.bat` (for Windows users), respectively `start-camunda.sh` (for Unix users).

This script will start the application server and open a welcome screen in your web browser. If the page does not open, go to [http://localhost:8080/camunda-welcome/index.html](http://localhost:8080/camunda-welcome/index.html).

{{< note title="Getting Help" class="info" >}}
If you have trouble setting up the Camunda BPM platform, you can ask for assistance in the [Camunda Users Forum](https://camunda.org/community/forum.html).
{{< /note >}}


# Camunda Modeler

Download the Camunda Modeler from [the download page](https://camunda.com/download/modeler/).

After having downloaded the modeler, just unzip the download in a folder of your choice.

After you have successfully unpacked the zip, run `camunda-modeler.exe` (for Windows users), respectively `camunda-modeler.app` (for Mac users) or `camunda-modeler.sh` (for Linux users).
