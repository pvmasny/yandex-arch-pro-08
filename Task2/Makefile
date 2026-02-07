start:
	minikube start
	minikube status
	minikube addons enable metrics-server
part_1:
	kubectl apply -f ./deploy/namespace.yaml
	kubectl apply -f ./deploy/deployment.yaml
	kubectl apply -f ./deploy/service.yaml
	kubectl apply -f ./deploy/hpa.yaml
part_2:
	kubectl apply -f ./deploy/namespace.yaml
	kubectl apply -f ./deploy/deployment.yaml
	kubectl apply -f ./deploy/service.yaml
	kubectl apply -f ./deploy/service-monitor.yaml

	helm install prometheus-adapter prometheus-community/prometheus-adapter -n monitoring -f ./deploy/prometheus-adapter.yaml
	kubectl apply -f ./deploy/hpa-rps.yaml

prometheus:
	kubectl port-forward service/prometheus-kube-prometheus-prometheus -n monitoring 9090:9090

scaletest:
	kubectl port-forward service/scaletestapp-svc 8080:80 -n insuretech


dash:
	minikube dashboard
clean:
	kubectl delete pods,deployments -A --all
	kubectl delete ns monitoring --wait
	kubectl delete ns insuretech --wait