# Summary 
Each account has a Registry, each Registry can contain several repositories. Each Repository can contain several Images. An image can have Several Tags, a Tag can only exist once per Repository.


## Components of Amazon ECR

* Registry
An Amazon ECR private registry is provided to each AWS account; you can create one or more repositories in your registry and store images in them. For more information, see Amazon ECR private registry.

* Authorization token
Your client must authenticate to Amazon ECR registries as an AWS user before it can push and pull images. For more information, see Private registry authentication.

* Repository
An Amazon ECR repository contains your Docker images, Open Container Initiative (OCI) images, and OCI compatible artifacts. For more information, see Amazon ECR private repositories.

* Repository policy
You can control access to your repositories and the images within them with repository policies. For more information, see Private repository policies.

* Image
You can push and pull container images to your repositories. You can use these images locally on your development system, or you can use them in Amazon ECS task definitions and Amazon EKS pod specifications. For more information, see Using Amazon ECR images with Amazon ECS and Using Amazon ECR Images with Amazon EKS.