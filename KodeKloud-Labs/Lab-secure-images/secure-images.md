## pdate the image of the deployment to use a new image from myprivateregistry.com:5000
`kubectl set image deployments/web nginx=myprivateregistry.com:5000/nginx:alpine `

## Create Docker secret:
- Name: private-reg-cred
- Username: dock_user
- Password: dock_password
- Server: myprivateregistry.com:5000
- Email: dock_user@myprivateregistry.com

```
kubectl create secret docker-registry private-reg-cred \
--docker-server=myprivateregistry.com:5000 \
--docker-username=dock_user \
--docker-password=dock_password \
--docker-email=dock_user@myprivateregistry.com
```

## Configure the deployment to use credentials from the new secret to pull images from the private registry

```
k edit deployments.apps web

   spec:
      containers:
      - image: myprivateregistry.com:5000/nginx:alpine
        imagePullPolicy: IfNotPresent
        name: nginx
      imagePullSecrets:
      - name: private-reg-cred
```