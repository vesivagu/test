apiVersion: apps/v1
kind: Deployment
metadata:
  name: mock-server
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mock-server
  template:
    metadata:
      labels:
        app: mock-server
    spec:
      containers:
        - name: mock-server
          image: node:18-alpine
          command: ["sh", "-c"]
          args:
            - |
              npm install -g @your-scope/your-mock-server && \
              your-mock-server --port 7878
          ports:
            - containerPort: 7878
          volumeMounts:
            - name: npmrc-volume
              mountPath: /root/.npmrc
              subPath: .npmrc
      volumes:
        - name: npmrc-volume
          configMap:
            name: mock-npmrc
---
apiVersion: v1
kind: Service
metadata:
  name: mock-server
spec:
  selector:
    app: mock-server
  ports:
    - protocol: TCP
      port: 80
      targetPort: 7878
---
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: mock-server
spec:
  to:
    kind: Service
    name: mock-server
  port:
    targetPort: 80
  tls:
    termination: edge
