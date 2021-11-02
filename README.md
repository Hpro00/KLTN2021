# KLTN2021
Hello, I'm Hieu. Here is my Graduate thesis about Apache Storm on Kubernetes
If you want to use my image in K8s
Remember when submitting your Storm jar topo, you have to use hostPort for upload because if not you can't send to nimbus:6627!
One more thing: my image base on image from mattf and build on ubuntu with hard-codede port and nimbus.seeds. Finally, i used alpine for reduce size of image.
