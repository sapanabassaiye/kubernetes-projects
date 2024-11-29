
# Deployment Steps for Flask-MongoDB Application on K3S

Prerequisites
•	K3S installed and running
reference: https://docs.k3s.io/quick-start

•	Docker installed
reference: https://docs.docker.com/engine/install/

**Note: All the files required for the application are available in main file**

Steps:
1.	Check status of cluster node:<br/>
`kubectl get nodes`

2.	 Build docker image: 
•	Navigate to the application directory.<br/>
•	Build the Docker image:<br/>
	`docker build -t flask-mongo-app . `<br/>
•	Login to docker hub<br/>
`docker login`<br/>
•	Tag the image under docker hub username<br/>
`docker tag flask-mongo-app:latest username/flask-mongo-app:latest`<br/>
•	Push tagged image to docker hub<br/>
`docker push username/flask-mongo-app:latest`

3.	Create namespace:
•	Create separate namespace for application<br/>
`kubectl create namespace flask-mongo-app`

4.	Deploy Flask Application:
•	Apply hpa.yml, flask-dep.yml and flask-svc.yml files in above created namespace<br/>
`kubectl apply -f /flask-mongo-app/flaskapp-files/ -n flask-mongo-app`

5.	Deploy MongoDB:
•	Apply first secret.yml file then apply mongodb-statefulset.yml and mongodb-service.yml in above created namespace<br/>
`kubectl apply -f /flask-mongo-app/mongodb-files/secret.yml -n flask-mongo-app`<br/>
`kubectl apply -f /flask-mongo-app/mongodb-files/mongodb-statefulset.yml -n flask-mongo-app`<br/>
`kubectl apply -f /flask-mongo-app/mongodb-files/mongodb-service.yml -n flask-mongo-app`<br/>

6.	Access the Flask Application:
•	Retrieve the NodePort assigned to the Flask service<br/>
`kubectl get svc -n flask-mongo-app`<br/>
`curl localhost:node-port`

7.	Test the application
•	To post data<br/>
`curl -X POST -H “Content-Type: application/json” -d ‘{“sampleKey”:”sampleValue”}’ http://user:password@localhost:node-port/data`<br/>
•	To retrieve data<br/>
`curl localhost:node-port/data`
