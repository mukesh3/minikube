Working with deployments
Run below command to create deployment </br>
```# kubectl create -f demo-deployment.yml --save-config --record
# kc get rs -o wide
NAME                    DESIRED   CURRENT   READY     AGE       CONTAINERS   IMAGES         SELECTOR
demo-nginx-5b8668b4c6   3         3         3         30s       demo-nginx   nginx:1.11.0   pod-template-hash=5b8668b4c6,run=demo-nginx

Now for updating the replicas use below:
# kubectl set image deployment demo-nginx demo-nginx=nginx:1.12.0 --record

# kc get rs -o wide
NAME                    DESIRED   CURRENT   READY     AGE       CONTAINERS   IMAGES         SELECTOR
demo-nginx-5b8668b4c6   0         0         0         1m        demo-nginx   nginx:1.11.0   pod-template-hash=5b8668b4c6,run=demo-nginx
demo-nginx-8884db599    3         3         3         11s       demo-nginx   nginx:1.12.0   pod-template-hash=8884db599,run=demo-nginx

Same can be updated by yml file, change image version in demo-deployment.yml to ```image: nginx:1.12.2```
# kubectl apply -f demo-deployment_1.12.2.yml --record
# kc get rs -o wide
NAME                    DESIRED   CURRENT   READY     AGE       CONTAINERS   IMAGES         SELECTOR
demo-nginx-5b8668b4c6   0         0         0         3m        demo-nginx   nginx:1.11.0   pod-template-hash=5b8668b4c6,run=demo-nginx
demo-nginx-847659d685   3         3         3         1m        demo-nginx   nginx:1.12.2   pod-template-hash=847659d685,run=demo-nginx
demo-nginx-8884db599    0         0         0         2m        demo-nginx   nginx:1.12.0   pod-template-hash=8884db599,run=demo-nginx

# kubectl rollout history deployment demo-nginx
deployments "demo-nginx"
REVISION  CHANGE-CAUSE
1         kubectl create --filename=demo-deployment.yml --save-config=true --record=true
2         kubectl set image deployment demo-nginx demo-nginx=nginx:1.12.0 --record=true
3         kubectl apply --filename=demo-deployment_1.12.2.yml --record=true


# kubectl rollout undo deployment demo-nginx --to-revision=2
deployment "demo-nginx" rolled back
# kc get rs -o wide
NAME                    DESIRED   CURRENT   READY     AGE       CONTAINERS   IMAGES         SELECTOR
demo-nginx-5b8668b4c6   0         0         0         8m        demo-nginx   nginx:1.11.0   pod-template-hash=5b8668b4c6,run=demo-nginx
demo-nginx-847659d685   0         0         0         5m        demo-nginx   nginx:1.12.2   pod-template-hash=847659d685,run=demo-nginx
demo-nginx-8884db599    3         3         3         7m        demo-nginx   nginx:1.12.0   pod-template-hash=8884db599,run=demo-nginx
```


