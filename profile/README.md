# GitHub Actions Workflows 🚀

Esta organização tem como objetivo agrupar workflows reaprovetáveis do GitHub Actions. Aqui você irá encontrar workflows para Python, Docker, Terraform, AWS Beanstalk, AWS Lambda entre outros. A maioria dos workflows são apenas wrappers de outras actions abstraídos para facilitar a utilização em outros projetos.

## Repositórios em destaque ✅

* [Python Workflows](https://github.com/gh-actions-workflows/python-workflows)
* [Docker Workflows](https://github.com/gh-actions-workflows/docker-workflows)
* [Terraform Workflows](https://github.com/gh-actions-workflows/terraform-workflows)
* [Deploy AWS Lambda](https://github.com/gh-actions-workflows/aws-lambda-workflows)

## Exemplo de uso 💯

Workflow para verificação de código Python com Flake8 e Pytest, e deploy no AWS Lambda.

```yaml
name: Python Workflow
on: [push]

jobs:
  lint:
    uses: gh-actions-workflows/python-workflows/.github/workflows/flake8.yaml@1.2
    with:
      python-version: '3.10' 

  test:
    needs: lint
    uses: gh-actions-workflows/python-workflows/.github/workflows/pytest.yaml@1.2
    with:
      python-version: '3.10' 

  deploy:
    needs: test
    uses: gh-actions-workflows/aws-lambda-workflows/.github/workflows/deploy-lambda.yaml@1.6
    with:
      function_name: binance_trades
      handler: handler.handler 
    secrets:
      aws_access_key_id: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws_secret_access_key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      aws_region: ${{ secrets.AWS_REGION }
```

## Informações de contato 📞

<a href="https://www.linkedin.com/in/pedro-henrique-pereira-almeida/" target="_blank"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank"></a> 
<a href = "mailto:pedro.6571almeida@gmail.com"><img src="https://img.shields.io/badge/-Gmail-%23333?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
