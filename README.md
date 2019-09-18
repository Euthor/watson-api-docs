# watson-api-docs
EuComply/Watson API Documentation


### Install dependencies:

Install [calamum](https://github.com/malachheb/calamum).

```bash
$ gem install specific_install
$ gem specific_install https://github.com/malachheb/calamum
```

### Edit API Definition and generate docs:

Edit `api-definition.json` then:

```bash
# IMPORTANT: Change the -p value to YOUR appropriate path.
$ calamum -f api-definition.json -t twitter -p /Applications/MAMP/htdocs/watson-api-docs
```

The docs should be generated in `/docs` directory as a Bootstrap template.

### Authors

- Nicholas Kyriakides, @nicholaswmin
