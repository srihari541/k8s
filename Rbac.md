

# To create a private key for your new certificate user
    openssl genrsa -out srihari.key  
# To create a certificate signed request 
 openssl req -new -key srihari.key -out srihari.csr -subj "/CN=srihari/O=dev/O=example.org"

# This certificate signed request must be signed by certificate authority.
# you can get certificate authourity details from kubeconfig  files.
sudo openssl x509 -req -CA ~/.minikube/ca.crt -CAkey ~/.minikube/ca.key -CAcreateserial -days 730 -in srihari.csr -out srihari.crt
#using the above command you can generate certificate
# Now you can add the users to your cluster config using below command
 kubectl config set-credentials srihari --client-certificate=srihari.crt --client-key=srihari.key
 # To create the context
  kubectl config set-context srihari-minikube --cluster=minikube --user=srihari --namespace=default
# kubectl config get-contexts
# kubectl config use-context srihari-minikube
#to ender into pod/ kubectl exec -it  <pod-name> -- bash

