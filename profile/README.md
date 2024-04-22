# GitHub Actions Workflows 🚀

Esta organização tem como objetivo agrupar workflows reaprovetáveis do GitHub Actions. Aqui você irá encontrar workflows para Python, Docker, Terraform, AWS Beanstalk, AWS Lambda entre outros. A maioria dos workflows são apenas wrappers de outras actions abstraídos para facilitar a utilização em outros projetos.

## Repositórios em destaque ✅

* [Deploy Render](https://github.com/gh-actions-workflows/deploy-docker-render)
* [Java Workflows](https://github.com/gh-actions-workflows/java-workflows)
* [Python Workflows](https://github.com/gh-actions-workflows/python-workflows)
* [Docker Workflows](https://github.com/gh-actions-workflows/docker-workflows)
* [Terraform Workflows](https://github.com/gh-actions-workflows/terraform-workflows)
* [Deploy AWS Lambda](https://github.com/gh-actions-workflows/aws-lambda-workflows)

## Exemplos de uso 💯

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

Workflow para verificação de código Python com Flake8 e Pytest, e deploy no Render.

```yaml
name: My Workflow
on: [push]

jobs:
  lint:
    uses: gh-actions-workflows/python-workflows/.github/workflows/flake8.yaml@master

  test:
    needs: lint
    uses: gh-actions-workflows/python-workflows/.github/workflows/pytest.yaml@master

  publish:
    uses: gh-actions-workflows/docker-workflows/.github/workflows/docker-publish.yaml@v1.0
    if: ${{ github.ref_name == 'master' || github.ref_name == 'develop'}}
    needs: test
    with:
      app_name: 'my-app'
      docker_hub_user: ${{ vars.DOCKER_HUB_USER }}
    secrets:
      docker_hub_password: ${{ secrets.DOCKER_HUB_PASSWORD }}

  deploy:
    if: ${{ github.ref_name == 'master' }}
    needs: publish
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Render
        uses: gh-actions-workflows/deploy-docker-render@v1.3
        with:
          deploy-hook: ${{ secrets.RENDER_DEPLOY_HOOK }}
          image-url: ${{ needs.publish.outputs.image_name }}
          render-api-key: ${{ secrets.RENDER_API_KEY }}
          wait-for-deployment: true
```

## Informações de contato 📞

<a href="https://www.linkedin.com/in/pedro-henrique-pereira-almeida/" target="_blank"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank"></a> 
<a href = "mailto:pedro.6571almeida@gmail.com"><img src="https://img.shields.io/badge/-Gmail-%23333?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
