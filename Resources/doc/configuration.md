# Configuration tree

Here's an example of full configuration with all possible options including default values:

```yml
ongr_elasticsearch:
    analysis:
        analyzer:
            pathAnalyzer:
                type: custom
                tokenizer: pathTokenizer
        tokenizer:
            pathTokenizer:
                type : path_hierarchy
                buffer_size: 2024
                skip: 0
                delimiter: /
        filter:
            incremental_filter:
                type: edge_ngram
                min_gram: 1
                max_gram: 20
    managers:
        default:
            index: 
                hosts:
                    - 127.0.0.1:9200
                index_name: ongr-default
                settings:
                    refresh_interval: -1
                    number_of_replicas: 0
                    number_of_shards: 1
            logger: true #default %kernel.debug%
            mappings:
                - AcmeBarBundle #Scans all bundle documents
        custom:
            index: 
                hosts:
                    - 10.0.0.1:9200 #default 127.0.0.1:9200
                index_name: ongr-custom
                mappings:
                    AcmeBundle:
                        document_dir: Document
```

Advanced `hosts` configuration (as seen in the [Extended Host Configuration](https://www.elastic.co/guide/en/elasticsearch/client/php-api/current/_configuration.html#_extended_host_configuration) of the Elasticsearch-PHP configuration guide):
```yml
ongr_elasticsearch:
    managers:
        default:
            index:
                hosts:
                    - 127.0.0.1:9200
                    - https://username:password@asdzxc-456123.eu-west-1.bonsaisearch.net
                    -
                        host: 127.0.0.1
                        port: 9200
                    -
                        host: asdzxc-456123.eu-west-1.bonsaisearch.net
                        port: 443
                        scheme: https
                        user: username
                        pass: password
```
