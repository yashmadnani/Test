apiVersion: apps/v1
kind: Deployment
metadata:
  name: pipelinex-app
  labels:
    app: pipelinex
spec:
  replicas: 2
  selector:
    matchLabels:
      app: pipelinex
  template:
    metadata:
      labels:
        app: pipelinex
    spec:
      containers:
      - name: pipelinex-app
        image: pipelinex/app:latest
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: pipelinex-service
spec:
  selector:
    app: pipelinex
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: LoadBalancer
