# udemy
For learning
https://viblo.asia/p/kubernetes-series-bai-4-services-expose-traffic-cho-pod-Ljy5VDm9Zra


Lab:
-	BE: API get dữ liệu từ DB, hiển thị trên FE
-	DB: mongoDB
-	Viết dockerfile cho FE BE DB (cài từ ubuntu)
-	
-	Dựng trên cụm K8S, 
-	truy cập FE từ domain và IP của master node
-	Chạy trên cùng 1 namespace
-	DB: chạy trên worker 3
-	FE, BE: mỗi loại 2 pods
-	
-	Mỗi node chỉ có 1 pod chạy BE, FE tương tự 
-	Node nào có BE thì phải có FE trên đó
-	Rolling update cho FE và BE, mỗi lần restart chỉ 1 pod bị xoá
-	
-	Dùng configmap và secret
-	Pod DB: volume là EBS, dùng dynamicProvision
