# Read me

The original idea is from  
https://dzone.com/articles/why-is-kubernetes-debugging-so-problematic

1. Start App
   Use debug agent

```
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar myapp.jar
```

2. Port Forwarding
   Use port forwarding

 ````
   kubectl port-forward <pod-name> 5005:5005
   ````

3. Remote Debugging
   In your IDE (e.g., IntelliJ IDEA, Eclipse), set up a remote debugging configuration. Specify the host as localhost
   and the port as 5005.