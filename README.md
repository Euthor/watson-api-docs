# watson-api-docs
EuComply/Watson API Documentation


## View the Docs (for external users)

Visit: https://euthor.github.io/watson-api-docs/docs/


## Edit Docs (for Euthor developers)

### Install dependencies:

Install [calamum](https://github.com/malachheb/calamum).

```bash
$ gem install specific_install
$ gem specific_install https://github.com/malachheb/calamum
```

### Edit API Definition and generate docs:

Edit `api-definition.json` then:

```bash
$ calamum -f api-definition.json -t twitter -p ${PWD}
```

The docs should be generated in `/docs` directory as a Bootstrap template.

### Authors

- Nicholas Kyriakides, @nicholaswmin
