# Codecov on Azure pipelines
Example for setting up CI on Azure with the new Codecov uploader.

1) Add `azure-code-coverage.yml` to your repository.
2) Have steps that generate the code coverage data for your project.
3) Add a step in your CI YAML file to install and run the uploader:
```
- template: azure-code-coverage.yml
  parameters:
    name: upload_coverage
    displayName: 'Upload code coverage'
```
4) Set `CODECOV_TOKEN` on Azure with your Codecov token as a secret variable!
5) Set `CODECOV_PUBLIC_KEY` variable on Azure with Codecov's base 64 encoded PGP key [keys/codecov-pgp-64encoded.asc](keys/codecov-pgp-64encoded.asc) or:
   1) Download their PGP key.
   2) Run `base64 -i input-file -w 0 > output.file`
6) Commit all changes and let the CI run. 

### Important: If you change the values of the variables on Azure you need to commit again in order for the CI to use the new ones. Restarting a failed job will use the old values!