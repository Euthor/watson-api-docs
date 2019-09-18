# watson-api-docs
EuComply/Watson API Documentation

## View the Docs (for external users)

- Visit https://euthor.github.io/watson-api-docs/ to view the documentation.

## Edit Docs (for Euthor developers)

### Install dependencies:

Install [calamum](https://github.com/malachheb/calamum). The published gem
doesn't actually correspond to latest master so we have to bundle directly
from Github:

```bash
$ gem install specific_install
$ gem specific_install https://github.com/malachheb/calamum
```

### Edit API Definition and generate docs:

Edit `api-definition.json` then:

```bash
$ sh build.sh
```

The docs should be generated in `/docs` directory.

### Authors

- [Nicholas Kyriakides, @nicholaswmin](https://github.com/nicholaswmin)
