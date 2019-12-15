# Docker for GCP operations
This docker is having
- Google cloud SDK
- Terraform
- firebase-tools


# Usage

```bash
docker-compose up -d

docker exec -it gcpope /bin/bash

docker-compose down
```

- gcloud

```bash
# インストールされているコンポーネントの詳細を見ることができます。
gcloud components list

# インストールされているコンポーネントをアップデートします。
gcloud components update

# App Engine SDK for Java のインストール
# gcloud components install app-engine-java
```



# References

- Cloud SDK > [Installing with yum (Red Hat and CentOS)](https://cloud.google.com/sdk/docs/downloads-yum)
- [Installing Terraform](https://learn.hashicorp.com/terraform/getting-started/install.html)
