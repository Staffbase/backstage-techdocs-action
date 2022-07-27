# 📖 GitHub Action for Backstage TechDocs

This GitHub Action can be used for generating and publishing [Backstage TechDocs](https://backstage.io/docs/features/techdocs/techdocs-overview).

## Features

The action facilitated [TechDocs CLI](https://backstage.io/docs/features/techdocs/cli) to generate and publish TechDocs sites.

- Building TechDocs only
- Building and publish TechDocs to cloud object storage
  - AWS S3
  - Azure Blob

## Usage

The following shows a minimal example of building and publishing TechDocs to AWS S3.

```yaml
name: Publish TechDocs Site

on:
  push:
    branches:
      - main
    paths:
      - "docs/**"
      - "mkdocs.yml"

jobs:
  publish-techdocs-site:
    name: Publish TechDocs Site
    runs-on: ubuntu-20.04
    steps:
      - name: Setup Node
        uses: Staffbase/backstage-techdocs-action@v1
        with:
          entity-name: 'pizza-service'
          publisher-type: 'awsS3'
          storage-name: 'staffbase-backstage-techdocs'
          aws-access-key-id: ${{ secrets.TECHDOCS_AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.TECHDOCS_AWS_SECRET_ACCESS_KEY }}
```

## Configuration

| Name                    | Description                                                                          | Required | Default        |
| ----------------------- | ------------------------------------------------------------------------------------ | -------- | -------------- |
| `entity-namespace`      | Entity namespace in Backstage                                                        | `true`   | `default`      |
| `entity-kind`           | Kind of the Backstage entity                                                         | `true`   | `Component`    |
| `entity-name`           | Name of the Backstage entity                                                         | `true`   |                |
| `publisher-type`        | One of `awsS3 | azureBlobStorage`. If not set, generated site will not be published. | `false`  |                |
| `storage-name`          | In case of AWS, use the bucket name. In case of Azure, use container name.           | `false`  |                |
| `aws-region`            | **Required if `publisher-type: awsS3`** AWS Region                                   | `false`  | `eu-central-1` |
| `aws-access-key-id`     | **Required if `publisher-type: awsS3`** AWS Access Key ID                            | `false`  |                |
| `aws-secret-access-key` | **Required if `publisher-type: awsS3`** AWS Secret Access Key                        | `false`  |                |
| `azure-account-name`    | **Required if `publisher-type: azureBlobStorage`** Azure Account Name                | `false`  |                |
| `azure-account-key`     | **Required if `publisher-type: azureBlobStorage`** Azure Account Key                 | `false`  |                |

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## License

This project is licensed under the Apache-2.0 License - see the [LICENSE.md](LICENSE) file for details.

<table>
  <tr>
    <td>
      <img src="assets/staffbase.png" alt="Staffbase GmbH" width="96" />
    </td>
    <td>
      <b>Staffbase GmbH</b>
      <br />Staffbase is an internal communications platform built to revolutionize the way you work and unite your company. Staffbase is hiring: <a href="https://jobs.staffbase.com" target="_blank" rel="noreferrer">jobs.staffbase.com</a>
      <br /><a href="https://github.com/Staffbase" target="_blank" rel="noreferrer">GitHub</a> | <a href="https://staffbase.com/" target="_blank" rel="noreferrer">Website</a> | <a href="https://jobs.staffbase.com" target="_blank" rel="noreferrer">Jobs</a>
    </td>
  </tr>
</table>
