
# PID 1 Problem

Die App wird im Container gestartet, aber nicht richtig beendet. Unter Linux wird dann ein SIGKILL gesendet, welches die APP killt. Das ist schlecht, weil die APP gerade ein File schreiben könnte, das dann inkonsistent ist. Weitere Info unter diesem [Link](https://www.padok.fr/en/blog/docker-processes-container). **Zusätzlich**, benötigt der Cotainer länger beim runter fahren, was im Kubernetes Fall ein längeres Update zu Folge hat.

#Docker 