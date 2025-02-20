Static Volume - EBS:

1. Create EBS volume in AWS
2. assign ebscsidrivepolicy role to one of the nodes 
3. ebs volume should be nodes AZ
4. install EBS volume drivers on cluster = kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.39"
5. Now create PV(Persistant Volume) in K8s cluster so it act as ebs volume inside k8s.
6. To cliam this volume - need to write PVC(Persistant volume claim) 
7. Mention this inside pod with Volume and inside container as volumeMounts 

Dynamic volume - EBS: 

1.  Storage class created by admins 
2.  While crerating PVC we give Storage class 
3.  When kubectl apply pvc it automatically/dynamically creates PV and external volume AWS EBS

EFS - static: (NFS)

1. create NFS in aws in same as cluster VPC
2. NFS has Security group, so allow inbound and outbound to NFS from cluster security group
3. install EFS drivers and check IAM role (AmazonEfsCsiPolicy) for access.
4. kubectl kustomize \
    "github.com/kubernetes-sigs/aws-efs-csi-driver/deploy/kubernetes/overlays/stable/ecr/?ref=release-2.1" > private-ecr-driver.yaml
5. kubectl apply -f private-ecr-driver.yaml

EFS - dynamic : 

1. 
